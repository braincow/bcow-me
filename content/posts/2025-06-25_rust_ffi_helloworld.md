+++
title = "Let's learn about Rust C bindings and FFI"
weight = 0
updated = 2025-08-10

[taxonomies]
tags = ["rust", "C"]
+++

## Bridging worlds

I have for a while now wondered about how Rust and C interoperate, not for any other reason than intrigue and trying to figure out how the damn thing works.

Therefore I ventured into the exciting world of the Foreign Function Interface, or FFI. It's a powerful feature that allows Rust to communicate with other programming languages, and a great way to understand this is to write an interface yourself. And so I did. I will be deconstructing the work I did over midsummer this year, creating a simple C-library for "Hello, World!" messages and then writing Rust bindings for it.

Since I really did not know what the hell I was doing initially, I ended up using Gemini Code Assist to bridge the gaps, or chasms, in my knowledge during the excercise.

### FFI

In simple terms, the Foreign Function Interface (FFI) is a mechanism that allows code written in one programming language to call, and be called by code written, in another language. In the context of Rust, FFI is most commonly used to interoperate with C libraries. This is because C has a well-defined Application Binary Interface (ABI), which makes it a common denominator for interoperability between many languages.

#### Why is FFI a Big Deal?

Rust's FFI opens up a world of possibilities:

* **Leveraging Existing Ecosystems:** You don't have to reinvent the wheel. There are countless high-quality and battle-tested libraries written in C. With FFI, you can use them directly in your Rust projects.
* **Performance-Critical Code:** While Rust is already incredibly fast, you might have a legacy C library that's highly optimized for a specific task. FFI allows you to call that library from your Rust code, getting the best of both worlds.
* **Gradual Modernization:** FFI is perfect for gradually migrating a legacy codebase to Rust. You can start by rewriting small parts of your application in Rust and use FFI to bridge the old and new code.

## A "Hello, World!" Example

My "hello world" code is available in its entirety on [GitHub](https://github.com/braincow/rust_ffi_helloworld). While FFI interface in my understanding could also provide bi-directional function calls e.g. C-code could call a Rust function, in this excersise we only implement exposed C-functions to Rust code.

### A C-library

First, we need a simple C-library and a function that the C-library will expose.

In `src/hello.h` we define a simple C-function called "hello":

```c
#include <stddef.h> // For size_t

// Writes a greeting into the provided buffer.
// Returns the number of bytes written (excluding the null terminator), or -1 on error.
int hello(const char *name, char *out_buffer, size_t buffer_len);
```

And in `src/hello.c` we implement the "hello" function itself:

```c
#include "hello.h" // Include our header file
#include <stdio.h> // For snprintf

int hello(const char *name, char *out_buffer, size_t buffer_len)
{
    // Use "World" as a default if the provided name is NULL or empty.
    const char *effective_name = (name != NULL && name[0] != '\0') ? name : "World";

    int written = snprintf(out_buffer, buffer_len, "Hello, %s\n", effective_name);

    if (written < 0 || (size_t)written >= buffer_len)
    {
        // An error occurred or the buffer was too small.
        return -1;
    }

    return written;
}
```

This function takes in a pointers for name and buffer to modify. Then with `sprintf` we construct a string "Hello Name" and push that into the buffer after which function returns with the number of bytes written, or -1 in case of an error. Pretty standard thread safe C-code stuff I think.

### Rust "sys" crate

In Rust we usually have a crate with suffix `-sys` that implements the FFI interface to C-code via bindings, in this case `hello-sys`. These bindings can be manually created I guess, but Rust also provides a `bindgen` crate that can automate this process.

To simplify proceedings a bit I created a `wrapper.h` header file that `#include`s the `hello.h` header file. In real life projects this would be the place where you would include all the other headers you need. I guess depending on your use case you could use many other paradigms here, but this seems to be somewhat "standard" way of managing the inclusion of C-functions.

Then on `hello-sys/build.rs` file we tell to the Cargo buildtool how to generate the bindings via `bindgen` crate:

```rust
fn main() {
    // --- Part 1: Define Header and Include Paths ---

    // The path to the source repository
    let hello_source_path = PathBuf::from("../src"); // Adjust this path if needed

    let hello_c_file = hello_source_path.join("hello.c");
    let wrapper_h_file = PathBuf::from("wrapper.h");
    let hello_h_file = hello_source_path.join("hello.h");

    println!("cargo:rerun-if-changed={}", wrapper_h_file.display());
    println!("cargo:rerun-if-changed={}", hello_c_file.display());
    println!("cargo:rerun-if-changed={}", hello_h_file.display());

    // --- Compile C code ---
    // This will compile hello.c and create a static library (e.g., libhello_c_lib.a)
    // The name "hello_c_lib" is arbitrary but should be consistent.
    cc::Build::new()
        .file(&hello_c_file)
        .include(&hello_source_path) // So hello.c can find hello.h if it needs to, and for bindgen's include context
        .compile("hello_c_lib");

    // --- Part 2: Configure bindgen ---

    let bindings = bindgen::Builder::default()
        // The header file we want to generate bindings for.
        // We use a "wrapper" header for better control.
        .header(wrapper_h_file.to_str().unwrap())
        // Tell cargo to invalidate the built crate whenever any of the
        // included header files changed.
        .parse_callbacks(Box::new(bindgen::CargoCallbacks::new()))
        // Add the necessary include paths for hello's internal headers.
        .clang_arg(format!("-I{}", hello_source_path.display())) // To find hello.h from wrapper.h
        // --- Part 3: Filter What to Generate (IMPORTANT) ---
        // By default, bindgen generates everything. hello headers include tons of
        // system headers. We should only allowlist the functions/types we need.
        // This makes the generated code smaller and compilation faster.
        .allowlist_function("hello")
        // Generate the bindings.
        .generate()
        .expect("Unable to generate bindings");

    // --- Part 4: Write the bindings to a file ---

    // Get the path to cargo's output directory.
    let out_path = PathBuf::from(env::var("OUT_DIR").unwrap());

    // Write the bindings to the $OUT_DIR/bindings.rs file.
    bindings
        .write_to_file(out_path.join("bindings.rs"))
        .expect("Couldn't write bindings!");

    // --- Part 5: Link the compiled C library ---
    println!("cargo:rustc-link-lib=static=hello_c_lib"); // Link the library we just compiled
}
```

Lots of things to unpack here, but most importantly:

1. It compile the `hello.c` and its function as `hello_c_lib` artifact via `cc` crate.
2. We generate the bindings for our C-library and with `.allowlist_function()` define that we wish to only include `hello` function instead of potentially everything present in the headers. This is somewhat redundant as we only have a single function defined in the `hello.h` header, but in real life you might want to limit the bindings generated to a just a subset of C-functions for example.
3. Annotate cargo build process with `cargo:rustc-link-lib=static=hello_c_lib` so that rustc will link the `hello_c_lib` artifact to the resulting Rust binary.
4. Also we annotate Cargo build process to rebuild the code if contents of `.c` or `.h` files change.

To incorporate the generated bindings to our Rust crate we, as a final step, need to include the generated code as part of our library.

`hello-sys/src/lib.rs` therefore contains:

```rust
// This brings the generated FFI declarations into our crate.
// The code will be located at $OUT_DIR/bindings.rs
// We must disable some lints that are commonly triggered by C code.
#![allow(non_upper_case_globals)]
#![allow(non_camel_case_types)]
#![allow(non_snake_case)]

include!(concat!(env!("OUT_DIR"), "/bindings.rs"));
```

Now when the `hello-sys` crate is built it will contain very unsafe, generated, code and includes the compiled C-library that does not bring any benefits of Rust to the table yet. This is handled by creating a safer library crate as an interface between the developer, sys crate and C-code.

### Rust crate

Naming convention aside this crate now uses the `hello-sys` crate created earlier to implement via `unsafe {}` code user friendly function implementations towards our C-code. So instead of using the `bindgen` generated functions the developer uses more "safe" and vetted code from this `hello-rs` crate instead.

In `hello-rs/src/lib.rs`:

```rust
pub fn hello(name: Option<&str>) -> Result<String> {
    // Convert the optional Rust &str to an optional C-compatible null-terminated string.
    // This will be `Some(CString)` if a name is provided, or `None` if the input is `None`.
    // `transpose()` converts `Option<Result<T, E>>` to `Result<Option<T>, E>`.
    let c_name_opt: Option<CString> = name
        .map(CString::new)
        .transpose()
        .context("CString::new failed due to interior null byte on parameter 'name'")?;

    // Get a pointer to the C string, or a null pointer if `name` was `None`.
    // The C function is designed to handle a null pointer gracefully.
    let name_ptr = match &c_name_opt {
        Some(s) => s.as_ptr(),
        None => std::ptr::null(),
    };

    // Create a buffer for the C function to write into.
    // We are responsible for allocating memory that the C code can use.
    let mut buffer: Vec<u8> = vec![0; 300];

    // Call the FFI function. The `unsafe` block is necessary because we are calling C code,
    // passing raw pointers, and trusting it to write safely into our buffer.
    unsafe {
        let written = hello_sys::hello(name_ptr, buffer.as_mut_ptr() as *mut c_char, buffer.len());

        if written < 0 {
            return Err(anyhow!(
                "C function 'hello' failed: the output buffer was too small."
            ));
        }

        // `written` is the number of bytes written (excluding the null terminator).
        let result_slice = &buffer[..written as usize];
        String::from_utf8(result_slice.to_vec())
            .context("Failed to convert C output to UTF-8 string")
    }
}
```

As we can see we still need to use `unsafe {}` code, but regardless of what you might have read in the Internet its _not_ wrong to use `unsafe` in Rust when you do it right. Hell, the Rusts standard library uses a lots of unsafe code. Most importantly in cases like this there is no way around it without fully re-implementing the C-library functionality in Rust natively, which misses the point of this excersise altogether. Real life is ugly and sometimes you just need to be reasonably unsafe.

So, if we are unsafe how can we mitigate the risks then? As we can see from the code snippet above I have created a Rust function `hello` that uses the sys crate provided unsafe `hello` function, but wraps it with sanity checks and transforms between C datatypes and native Rust datatypes while maintaining interoperability with the C-library functionality as much as possible. This way any potential documentation written for the C-code that describes parameters and function behavior stay the same across C and Rust implementations.

In the end when we make the calls to C-library via the unsafe code we should be doing things in a sane way, but how can we make sure that our assumptions are correct about "safeness"? Well, lets add some test cases of course:

```rust
#[cfg(test)]
mod tests {
    use super::*;

    #[test]
    fn say_hello() {
        let msg = hello(Some("Rust"));

        // Assert that the call was successful
        assert!(msg.is_ok());

        // Assert that the output is what we expect
        assert_eq!(msg.unwrap(), "Hello, Rust\n");
    }

    #[test]
    fn say_hello_to_world_on_empty_name() {
        // The C function treats an empty string as a case to default to "World".
        let msg = hello(Some(""));

        assert!(msg.is_ok());
        // Assert that an empty name defaults to "World"
        assert_eq!(msg.unwrap(), "Hello, World\n");
    }

    #[test]
    fn say_hello_to_world_on_none_name() {
        // Our Rust wrapper now passes NULL for None, and the C code defaults to "World".
        let msg = hello(None);
        assert!(msg.is_ok());
        assert_eq!(msg.unwrap(), "Hello, World\n");
    }

    #[test]
    fn check_internal_null_byte_error() {
        // C strings are null-terminated, so they cannot contain null bytes internally.
        // CString::new will return an error if this is attempted.
        let msg = hello(Some("Ru\0st"));
        assert!(msg.is_err());
        assert!(msg.unwrap_err().to_string().contains("interior null byte"));
    }

    #[test]
    fn succeeds_when_output_fits_exactly() {
        // The internal buffer in `hello` is 300 bytes.
        // The output format is "Hello, %s\n".
        // "Hello, " is 7 bytes.
        // "\n" is 1 byte.
        // The null terminator is 1 byte.
        // Total overhead is 9 bytes.
        // A name of (300 - 9) = 291 bytes will result in a 299-byte string,
        // which fits perfectly into the 300-byte buffer with its null terminator.
        let long_name = "a".repeat(291);
        let result = hello(Some(&long_name));

        assert!(result.is_ok());
        let expected = format!("Hello, {}\n", long_name);
        assert_eq!(result.unwrap(), expected);
    }

    #[test]
    fn fails_when_output_buffer_is_too_small() {
        // A name of 292 bytes will cause the C function to report an error because
        // the total output (7 + 292 + 1 = 300 bytes) plus the null terminator
        // requires a 301-byte buffer, but ours is 300.
        let long_name = "a".repeat(292);
        let result = hello(Some(&long_name));

        assert!(result.is_err(), "Expected an error, but got Ok");
        assert!(
            result
                .unwrap_err()
                .to_string()
                .contains("output buffer was too small")
        );
    }

    #[test]
    fn handles_multibyte_utf8_characters_correctly() {
        // "😊" is a 4-byte UTF-8 character. This test ensures that byte lengths,
        // not character counts, are handled correctly across the FFI boundary.
        let name = "😊";
        let msg = hello(Some(name));
        assert!(msg.is_ok());
        assert_eq!(msg.unwrap(), "Hello, 😊\n");
    }

    #[test]
    fn handles_input_with_c_format_specifiers() {
        // This is a defensive test. The C code uses `snprintf("...", name)`, which is safe.
        // An unsafe implementation might do `snprintf(name, ...)` with a user-controlled
        // string, which would be a format string vulnerability. This test confirms
        // our implementation is not vulnerable and treats specifiers as literals.
        let name = "user %s%s%n";
        let msg = hello(Some(name));
        assert!(msg.is_ok());
        assert_eq!(msg.unwrap(), "Hello, user %s%s%n\n");
    }
}
```

There is approximately 2x more test code than actual implementation code for the Rust `hello` function. Writing `unsafe` code is only unsafe if you dont know what your code is doing or you dont care enough to validate your assumptions. But since we can only write test cases for situations that we are aware of no test suite is never perfect and this is how we get the blue screens, core dumps and sad Macs from time to time. When this happens fixes are applied and test cases written to cover that error state and to safeguard against future regressions.

## Bonus: Fuzzing

To over simplify what fuzzing is to say that its a technique of sequentially feeding garbage to a datastructure that is processed in someway or another in hopes of getting a crash and then analyzing the error state, creating a fix and test case for it.

Since we can write test cases for inputs and outputs we know of at time of writing your code our test suites are only as good as our imaginations or guidelines are, but it does not hurt to double check. So, in addition to creating comprehensive test suite in Rust I also added fuzzing support for the `hello-rs` crate.

`hello-rs/fuzz/fuzz_targets/fuzz_hello.rs` implements a fuzzing target for our `hello` Rust function:

```rust
fuzz_target!(|data: &[u8]| {
    // The fuzzer provides raw bytes. Our function's public API expects a `&str`,
    // which must be valid UTF-8.
    // We'll try to convert the bytes to a UTF-8 string. If it's not
    // valid UTF-8, we simply skip this input, as it falls outside the
    // function's contract. The fuzzer will quickly generate another input.
    if let Ok(s) = std::str::from_utf8(data) {
        // We call the function with the fuzzer-generated string.
        // We don't need to check the result (Ok or Err). The goal of the
        // fuzzer is to find inputs that cause a panic, crash, or hang.
        let _ = hello(Some(s));
    }
});
```

This simple fuzzer _should_, to my understanding, catch a situation where some user input to the Rust `hello` function that calls `hello` in the sys crate that binds to C-library function called `hello` causes a panic or a crash we become aware of it. I left the implementation running for few days and was unable to get a crash out of my code; I guess its relative good then or my fuzzing target is just broken or I got lucky with the generated data not triggering an error.

## Conclusion

I think I now understand the FFI interface on a superficial level and can create a more complex real life example next or at the very least am able to debug existing crates a little better. Also I need to check if I can use this approach in emdedded development too; I have camera module that I would like to use from Raspberry Pi Pico W, but they only provide C-library for interfacing with the module and so far manually initializing and using it from `embassy-rs` environment has been a tricky proposition.

Fun times were had, new things learned, so a win-win.
