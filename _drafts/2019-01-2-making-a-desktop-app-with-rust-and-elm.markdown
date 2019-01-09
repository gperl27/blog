---
layout: post
categories: rust elm
---
The average reader of HackerNews(use link) may have noticed the popular rise of articles pertaining to Rust. Though also a fairly popular video game (use link), Rust is a programming language. Now I didn't want to say "systems-level" here because not only is that more scary-sounding, but also because it doesn't fairly define what Rust has to offer. I believe a better way to put it is *systems-capable*. This means being able to access functions and commands that your native machine has to offer, from reading and writing a file on your operating system to talking to your GPU. If you're a webdev (like myself), this doesn't quite sound like your typical CRUD-induced web-app type of a language (though of course you can(link here)).

The reason I wanted to give Rust a shot was to get a deeper understanding of lower-leveled computing; my prior experiences involved a couple problem sets in C from cs50(link) and making a print server in Electron (JavaScript).

For me, the best way to learn any new language or paradigm is to do a side project. Hence, I decided to make a video management interface that keeps track of video files across multiple external devices. I used Rust to a cache of file references and serve data to a desktop webview, which will serve up html and JavaScript. The project helps users who have many external devices with many files dispersed among them. Users don't have to remember which file is on which device, and can also quickly search and filter through all the files tracked from within the app.

## Starting Rust (Working Title)

### Learning

Though diving right into the project with docs by my side was enticing, Rust was just a bit too terse and foreign to wing it. Additionally, a co-worker recommended that I read the Rust book(link), which is exactly what I did. I, too, recommend anyone interested in Rust to read it; it is excellently written, updated regularly, and covers many non-Rust specific programming practices that any developer can learn from. 

### Writing Rust

We all know the difference between reading about something, and actually doing it. Reading through The Book, I went through some of the tutorial projects, so I was a tad familiar in writing Rust code. But finally it was time to sit down and do my own thing. 

Rust's compiler is the perfectionist that you want at your side. Though it is not *all-knowing* as far as understanding the intention of what your program needs to do, it knows what doesn't work and will tell you why. Your program won't compile if Rust deems it unsafe.

Though a bit foreign at first, Rust's syntax ended up being a pleasure to work with. It offers structs(link) and enums(link) for encapsulating systems. I also dabbled in using generics for an object-oriented-like approach, as well as using some `derived` traits, which can help further with code reuse. However, I did run into some roadblocks when attempting to use functional iterators like `map` on my own custom structs due to trait implementations, as well as complying with the strict borrowing system. Thankfully, the compiler will aid you in telling you where mutable and immutable borrows happen so you scope data properly; additionally, the requisite of `lifetimes` was needed sometimes when needing to explicitly describe how long some data needs to stay in memory.

### Cargo

Cargo is Rust's package manager and is a powerful tool. Cargo can check your code, run and build your program, run tests, and much more. I found it fairly easy to work with and manage dependencies. A Rust project is configured through a `Cargo.toml`. To install a library all you need to do is add `mylib = 1.0.0` under `[dependencies]` and run `cargo check`. All rust *crates* can be found at crate.io; it's an excellent ecosystem and most libraries I used were well documented and supported. I additionally made use of `cargo make`, a build tool that I utilized to write intialization scripts (I'll cover more of this further in the frontend section).

## The Elm Bridge

You might be thinking, how will we actually interact with the app? Well, I stumbled upon a library called webview(link) which supports two-way bindings between Rust and JavaScript. If you've ever used Electron, it's extremely similar to their IPCs, which allow you to pass messages from the frontend to the backend and visa-versa. The cool thing about using Rust is the ability to send and receive type-safe JSON; something you can't get out of the box with Electron. 

Now, in the spirit of type-safety and reliablility, I opted in to using Elm(link) for the frontend. Elm is a typed, functional programming language. The Elm compilier is quite friendly and readable, aiding preventing runtime-errors (no `Cannot read property *blah* of undefined`). Lately, I've been using a ton of Ramda(link) in JavaScript, as well as dabbled with Elixir previously, so Elm was an excellent choice to satiate and improve my FP prowess. The learning curve wasn't too steep. It's lisp-like syntax was a bit off-putting at first, but I eventually got the hang of it; the biggest realization I had was how functions only accepted one argument only at a time and curried it to the next input. So, composing functions you had to do something like:

```
MyFunc1 (MyInnerFunc thisIsYourData)
```

Additionally, I thoroughly enjoyed the document-update-view model that they employ. If you come from using Redux (or most other Flux patterns) in your frontends, you'll feel right at home. 

### Using Ports

One thing that wasn't too straightforward was how to call vanilla JavaScript functions in Elm. Remember, the webview we're using doesn't communicate between Rust and Elm, but Rust and JavaScript. Luckily, Elm offers a way to send one-way messages through ports(link). Using ports, we can make a bridge that goes from Rust to JavaScript to Elm and back the other way.

What this translates to is:

- Backend to Frontend
  - Rust => serialize into JSON => JavaScript/Elm port passes JSON through as a string => Elm deserializes JavaScript message

- Frontend to Backend
  - Elm serializes message into JSON => sends through a port => Rust deserialzes JavaScript Message

## Getting Things to Production

### The Cargo Side

### Frontend Scripting

### Cargo Make

### Native Builds

## Final Thoughts
Overall, I felt I had a quality codebase, with little known bugs. Some deeper topics I'd like to explore further would be traits and multi-threading in Rust; for Elm, it'd be trying out to make a full-blown Progressive Web App (link).

A huge thank you to minesweeper username here(lin   k), which I heavily used for reference in getting started on this project. Thanks also to x,y,z for the feedback on this article.