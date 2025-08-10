+++
title = "Tauri and Vuetify want to say Hello, World!"
weight = 0
draft = true

[taxonomies]
tags = ["rust", "vue", "vuetify", "typescript", "tauri"]
+++

## An example application

Tauri's getting started guide and intuitive tooling assist one to quickly create a new application from scratch, but that uses Vue only and does not incorporate Vuetify. It is ofcourse possible manually to add the dependency, initialize and take it into use, but it still requires writing lots of boiler plate in case we want to utilize Pinia store, automated imports, automated routing and etc in our application that are not part of Vuetify itself, but which I love on its default template.

What does provide these things from out of the box? You guessed it, Vuetifys own tooling which we will utilize here via `pnpm`, but you are free to use `npm`, `yarn` or any another pleathora of tools available for this purpose in the JavaScript world. (Btw, one of the reasons why I hate modern frontend development, but I digress)

![Init Vuetify](new_vuetify_from_template.png "Initialize Vuetify from template")

After initializing the Vuetify we need to add Tauri to the dependencies and as a part of the build process. But first, before we can do that, we need to have the Tauri utilities as well as the operating system and other development libraries installed as detailed in the Tauri's quickstart guide. Remind you that you need to have of course [Rust toolchain and Cargo](https://rustup.rs/) installed first too.

![Add Tauri](add_tauri_dependency.png "Add Tauri dependencies to your Vuetify application")

And lets add Tauri to the build process while were at it and initialize the Rust application side of things.

![Initialize Tauri](initialize_tauri.png "Initialize Tauri Rust application as part of your Vuetify project")

Now we should be ready to see the foundations of both Tauri and Vuetify in action by initiating a build of our software and running it.

```sh
pnpm tauri dev
```

![Run app](build_and_start_helloworld.png "Run the Hello World application for the first time")

There we have it; Rust created OS native Webview framework running in a window with Vue application running inside it with Vuetify candy on top. When allowing the Tauri to start from its default template it gives us a text field and a button and when pressed we are greeted with the traditional "Hello, World" message. Lets re-implement that next.
