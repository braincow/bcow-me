+++
title = "Tauri and Vuetify a shotgun wedding for cross environment GUI in Rust"
weight = 0

[taxonomies]
tags = ["rust", "vue", "vuetify", "typescript", "tauri"]
+++

## Rust and GUI

Rust has gained immense popularity for its performance, memory safety, and concurrency features, making it a top choice for systems programming, backend services, and command-line tools. However, when it comes to Graphical User Interfaces (GUIs), the ecosystem is still in a state of active development and hasn't yet reached the maturity of other language. While there are several promising native Rust GUI toolkits like `egui`, `iced`, and `slint`, there isn't a single, dominant, framework that has become the de-facto standard. This fragmentation and relative immaturity mean that developers often turn to a proven and powerful alternative: leveraging web technologies. Frameworks like Tauri allow developers to build the core application logic in Rust while using standard web front-end technologies like HTML, CSS, and JavaScript/TypeScript (or in this case, Vue with Vuetify) to create a rich, cross-platform user interface.

### Native and less native GUI frameworks

Especially `iced` suffers from lack of good documentation and examples. Whats going for `iced` however is that it is the basis for System76's new Desktop Environment "[Cosmic](https://system76.com/cosmic/)" that shows great promise, but is, as of writing this blog entry, still in early beta stages. There is an possibility that if Cosmic takes off in similar way as Gnome did in the wake of GIMP ang GTK back in the day then `iced` might see large adoption similarly in the future.

Of course you can interact with `Qt`, `GTK` and even `Tk` from Rust via [FFI](@/posts/2025-06-25_rust_ffi_helloworld.md), but their roots are in C and C++ and therefore they are from Rust point of view "unsafe" which leads to really funky wrappers and paradigms with not so intuitive memory and thread management. There are crates like [Relm4](https://relm4.org/) that improve this massively, but still the experience feels a bit clunky in my opinion.

Others like `slint` are half commercial meaning that in certain cases you have to pay to use it although their almost "late" Qt type of an approach seems intriquing to those coming from C++ world. `egui` on the other hand is fully open source, but has its own issues with usability in my opinion. However I do like it in general, but it still seems to be aimed to the game development community more than anything else and does require "lots" of boiler plate to be usable in a pure desktop application. Sometimes the requirement of 3D accelaration also can cause problems on running or building the software using `egui`.

## Web frameworks as desktop applications

The idea of using web technologies to build desktop applications is far from new and has been battle-tested by some of the most popular applications used today. Giants like Slack, Discord, Visual Studio Code, and even parts of Spotify are built using this very approach, most commonly with the Electron framework. The benefits are compelling: developers can leverage their existing knowledge of HTML, CSS, and JavaScript to build a single, cross-platform application from one codebase. This dramatically speeds up development time, simplifies maintenance, and ensures a consistent user experience across Windows, macOS, and Linux. Furthermore, the vast and mature ecosystem of web development provides an unparalleled selection of tools, libraries, and frameworks, enabling the creation of rich, modern, and highly interactive user interfaces that can be more difficult or time-consuming to achieve with traditional native toolkits.

What empowers web developers however is the preverbial [smorgasbord](https://en.wikipedia.org/wiki/Smorgasbord) of libraries and ready made componets that can be used to create intuitive and flexible user interfaces and experiences. Replicating same functionality in "native" tooling or in some other UI framework that does not have the components yet requires a lot more development effort to achieve.

As an example, implement a responsive map with layers and markers and polygon based geodata into your application and you soon fall in love with things like *)[Leaftlet](https://leafletjs.com/) and [Leaflet.FreeDraw](https://github.com/Wildhoney/Leaflet.FreeDraw). Implementing that from scratch can be painful and a long project when all you have to work with are your GUI toolkits base components for drawing things. Although for the most part in the closed software world you can buy licences for ready made components for some of these functionalities, but in this opinion piece we are talking in completely Open Source context only.

*) ["Slava Ukraini"](https://u24.gov.ua/)

### NodeJS ecosystem is a mess

Its not all roses though. Using NPM is always a risk from software supply chain hygieny perspective. The situation is a bit of a fubar to be honest and might lead you introducing security vulnerabilities to your software even without you knowning it quite easily as NPM packages tend to be spoofed or malicious code might be injected into them. Also those libraries are quite easily abandoned meaning that future builds of your software might be broken without rewrites being involved.

Oh, I hate the NodeJS ecosystem, passionately, because of its security risks and the usually poor code quality and documentation, but then again most of the OSS world is the same too. I'm looking at you `iced`.

## Best of both worlds

### Tauri

[Tauri](https://tauri.app/) is a modern framework for building lightweight, secure, and cross-platform desktop applications using web technologies for the frontend. Unlike Electron, which bundles a full Chromium instance with every application, Tauri leverages the operating system's native web-rendering engine (WebView2 on Windows, WebKit on macOS, and WebKitGTK on Linux). This architectural choice results in significantly smaller application bundles and lower memory consumption. The core of a Tauri application is written in Rust, allowing developers to build high-performance, memory-safe backends that can handle everything from complex business logic to direct system interactions. The frontend and backend communicate over a secure and efficient bridge, where Rust functions can be explicitly exposed and called from the JavaScript/TypeScript running in the webview, providing a seamless integration between the native power of Rust and the rich UI capabilities of the web.

### Vuetify

To build the user interface, we turn to [Vue](https://vuejs.org/) and [Vuetify](https://vuetifyjs.com/). Vue.js is a progressive and approachable JavaScript/TypeScript framework for building UIs, it has a gentle learning curve and powerful component-based architecture. Building on top of this solid foundation is Vuetify, a comprehensive UI component library that implements Google's Material Design specification. It provides a vast collection of pre-made, professionally designed, and highly customizable components—from buttons and forms to complex data tables and navigation drawers. Using Vuetify with Vue in a Tauri application is a powerful combination: it allows developers to rapidly assemble a beautiful, modern, and responsive user interface without having to write extensive CSS or build common UI elements from scratch. This frees up developers to focus on the core application logic in the Rust backend, while still delivering a polished, feature-rich, and native-feeling desktop experience.

Without Vuetify you can still design your own components and use them in your UI to provide UX, but why re-invent the wheel if not necessary?

## Conclusion

This unholy marriage should not be needed, but since it is I am happy we have Tauri and Vuetify, because they together genuainly solve a problem. And they solve it well in the landscape filled with half done, almost working, maybe functional GUI toolkits.

This is where the pragmatic union of Tauri and Vuetify shines. It's a powerful combination that acknowledges the strengths of two different worlds. By pairing a high-performance, memory-safe Rust backend with the vast, mature, and component-rich ecosystem of web development, we get the best of both. Tauri provides the lightweight, secure bridge to the desktop, avoiding the bloat of older frameworks, while Vuetify allows for the rapid creation of a beautiful, modern user interface.

This approach is not just a compromise,  it is a strategic choice. It empowers developers to build robust, feature-rich, cross-platform desktop applications *now*, without sacrificing the performance and safety guarantees of Rust at their core. While we look forward to the day a dominant native Rust GUI framework emerges, the combination of Tauri and Vuetify offers a genuinely excellent and productive path forward.

In the next part of the series, I plan to demonstrate how easy it is to bootstrap an application, run it, and understand how these two technologies work together in practice.
