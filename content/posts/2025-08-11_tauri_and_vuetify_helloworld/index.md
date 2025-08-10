+++
title = "Tauri and Vuetify want to say Hello, World!"
weight = 0
draft = true

[taxonomies]
tags = ["rust", "vue", "vuetify", "typescript", "tauri", "Android"]
+++

## An example application

Tauri's getting started guide and intuitive tooling assist one to quickly create a new application from scratch, but that uses Vue only and does not incorporate Vuetify. It is ofcourse possible manually to add the dependency, initialize and take it into use, but it still requires writing lots of boiler plate in case we want to utilize Pinia store, automated imports, automated routing and etc in our application that are not part of Vuetify itself, but which I love on its default template.

What does provide these things from out of the box? You guessed it, Vuetifys own tooling which we will utilize here via `pnpm`, but you are free to use `npm`, `yarn` or any another pleathora of tools available for this purpose in the JavaScript world.

One of the reasons why I hate modern frontend development is the distracting development tooling and the state of the NPM ecosystem in general. More on the reasoning in the [first part of this series](@/posts/2025-08-10_tauri_and_vuetify.md).

### A new Vuetify application

![Init Vuetify](new_vuetify_from_template.png "Initialize Vuetify from template")

After initializing the Vuetify we need to add Tauri to the dependencies and as a part of the build process. But first, before we can do that, we need to have the Tauri utilities as well as the operating system and other development libraries installed as detailed in the Tauri's quickstart guide. Remind you that you need to have of course [Rust toolchain and Cargo](https://rustup.rs/) installed first too.

### Add Tauri to the project

![Add Tauri](add_tauri_dependency.png "Add Tauri dependencies to your Vuetify application")

And lets add Tauri to the build process while were at it and initialize the Rust application side of things.

![Initialize Tauri](initialize_tauri.png "Initialize Tauri Rust application as part of your Vuetify project")

Some parts of the Tauri tooling do require some additional configuration here and there in the Vite configuration. Also things like the `@tauri-apps/api` npm library is not added to the "devDependencies" section of your `package.json`, but these can be solved with minor edits. It is recommended to check the recommendations for additional steps in the Tauri's quick start guide that explains these changes in greater detail. But even without these modifications an "Hello, World" can be achieved.

### Launch the Hello, World

Now we should be ready to see the foundations of both Tauri and Vuetify in action by initiating a build of our software and running it.

```sh
pnpm tauri dev
```

![Run app](build_and_start_helloworld.png "Run the Hello World application for the first time")

There we have it; a Rust created OS native window with Vue application running inside of a platform spesific webview. All decorated with Vuetify eye-candy and all the routing goodness happening in the background. Granted there is very little of that in display here yet as there are only few boxes and images present, but imagine utilizing all of the fabolous components available from the Vuetify project.

#### One more neat trick, Android

If you have the Android SDK and emulator setup properly first you can actually run `pnpm tauri android`, and your Tauri application will start as an Android app inside the emulator without no need for any extra code or configuration. That is a neat trick if you should need it, for reasons.

### Conclusion

When allowing the Tauri to start from its default template it gives us a text field and a button and when pressed we are greeted with the traditional "Hello, World" message. Lets re-implement that in the next part of the series.
