---
layout: post
categories: rust elm
---
The average reader of HackerNews(use link) may have noticed the popular rise of articles pertaining to Rust. Though also a fairly popular video game (use link), Rust is a programming language. Now I didn't want to say "systems-level" here because not only is that more scary-sounding, but also because it doesn't fairly define what Rust has to offer. I believe a better way to put it is *systems-capable*. This means being able to access functions and commands that your native machine has to offer, from reading and writing a file on your operating system to talking to your GPU. If you're a webdev (like myself), this doesn't quite sound like your typical CRUD-induced web-app type of a language (though of course you can(link here)).

The reason I wanted to give Rust a shot was to get a deeper understanding of lower-leveled computing; my prior experiences involved a couple problem sets in C from cs50(link) and making a print server in Electron (JavaScript).

For me,     the best way to learn any new language or paradigm is to do a side project. Hence, I decided to make a video management interface that keeps track of video files across multiple external devices. The inspiration here was due to noticing my dad jumbling among many different devices trying to find certain files and not quite knowing which device had which file.

## Learning Rust

Though diving right into the project with docs by my side was enticing, Rust was just a bit too terse and foreign to wing it. Additionally, a co-worker recommended that I read the Rust book(link), which is exactly what I did. I, too, recommend anyone interested in Rust to read it; it is excellently written, updated regularly, and covers many non-Rust specific programming practices that any developer can learn from. 

## Writing Rust

We all know the difference between reading about something, and actually doing it. Rust's compiler is the perfectionist that you want at your side. Though it is not *all-knowing* as far as understanding the intention of what your program needs to do, it knows what doesn't work and will tell you why. Your program won't compile if Rust deems it unsafe.

Though a bit foreign at first, Rust's syntax ended up being a pleasure to work with. It offers structs and enums for encapsulating systems or objects so-to-speak. I also dabbled in using generics for an object-oriented-like approach, as well as using some `derived` traits, which can help further with code reuse. However, I did run into some roadblocks when attempting to use functional iterators like `map` on my own custom structs due to trait implementations, as well as complying with the strict borrowing system. Thankfully, the compiler will aid you in telling you where mutable and immutable borrows happen so you scope data properly; additionally, the requisite of `lifetimes` was needed sometimes when needing to explicitly describe how long some data needs to stay in memory.

### Cargo

Cargo is Rust's package manager and is a powerful tool. Cargo can check your code, run and build your program, run tests, and much more. I found it fairly easy to work with and manage dependencies. A Rust project is configured through a `Cargo.toml`. To install a library all you need to do is add `mylib = 1.0.0` under `[dependencies]` and run `cargo check`. All rust *crates* can be found at crate.io; it's an excellent ecosystem and most libraries I used were well documented and supported. I additionally made use of `cargo make`, a build tool that I utilized to write intialization scripts (I'll cover more of this further in the frontend section).


- structs and generics unlike js & scripting
- traits kind of like interfaces
- liked the error handling and unwrapping - like swift
- cargo check
- using a cargo make script - frontend section?
- good ecosystem, reliable supported libraries

## The Elm Bridge

You might be asking, how will we actually interact with the app? 

- boscop's webview
  - port of go's
  - problem on windows in folder picker
  - ended up using NFD
- included create_html()
- ran into weird issues using html file
- elm
  - bridge
  - what is it
  - like redux
- json back and forth - like electron ipc
  - ports
- inspiration from minesweeper project

## Final Thoughts
- overall success
- really enjoyed using both rust and elm
- want to explore traits and larger rust projects
- elm lisp ended up being very reliable
- intrigued by elm PWA