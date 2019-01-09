---
layout: post
categories: rust elm
---
The average reader of [HackerNews](https://news.ycombinator.com/) may have noticed the popular rise of articles pertaining to Rust. Though also a fairly popular [video game](https://www.google.com/search?q=rust+game&rlz=1C5CHFA_enUS805US805&oq=rust+game&aqs=chrome..69i57.1588j0j1&sourceid=chrome&ie=UTF-8), Rust is a programming language. Now I didn't want to say "systems-level" here because not only is that sounds a bit scary, but also because it doesn't fairly define what Rust has to offer. I believe a better way to put it is *systems-capable*. This means being able to utilize functions and commands that your native machine has to offer, from reading and writing a file on your operating system to talking to your GPU. If you're a webdev (like myself), this doesn't quite sound like your typical CRUD-induced web-app type of a language (though of course [you can](https://rocket.rs/)).

The reason I wanted to give Rust a shot was to get a deeper understanding of lower-leveled computing; my prior experiences involved a couple problem sets in C from [cs50](https://www.edx.org/course/cs50s-introduction-computer-science-harvardx-cs50x) and making a print server in Electron (a way to make cross-platform apps using JavaScript).

For me, the best way to learn any new language or paradigm is to do a side project. Hence, I decided to make a video management app that keeps track of video files across multiple external devices. I used Rust to cache file references and serve data to a desktop webview, which will serve up HTML and JavaScript. However, I ended up using Elm to build the front end, which I'll expand more on later. The project helps users who have many external devices with many files dispersed among them. Users don't have to remember which file is on which device, and can also quickly search and filter through all the files tracked from within the app.

GIF HERE

## Starting Out

Though diving right into the project with docs by my side was enticing, Rust was just a bit too terse and foreign to wing it. Additionally, a co-worker recommended that I read the Rust [book](https://doc.rust-lang.org/book/) (*The Book*), which is exactly what I did. I, too, recommend anyone interested in Rust to read it; it is excellently written, updated regularly, and covers many non-Rust specific programming practices that any developer can benefit from. 

### Writing Rust

We all know the difference between reading about something, and actually doing it. Reading through *The Book*, I went through some of the tutorial projects, so I was a tad familiar in writing Rust code. But finally it was time to sit down and do my own thing. 

Rust's compiler is the perfectionist that you want at your side. Though it is not *all-knowing* as far as understanding the intention of what your program needs to do, it knows what doesn't work and will tell you why. Your program will not compile if Rust deems it unsafe.

Though a bit foreign at first, Rust's syntax ended up being a pleasure to work with. It offers structs, enums, generics, and many other excellent programming features you'll find from you favorite languages. Additionally, the [standard library](https://doc.rust-lang.org/std/) is extremely robust and, more often than not, it offers a utility that you are looking for.

I ran into some roadblocks when attempting to use functional iterators like `map` on my own custom structs due to trait implementations requirements. For example, if you wanted to `clone` a custom struct, you have define the requisite protocols so the compilier knows how to iterate through your data safely. Additionally, I encountered some difficulty trying to mutate data structures in iterators due to the strict borrowing system; more often than not, I ended up either `cloning` data when needing to do filtering and other processes or creating a new `vec!` (like an array), using a for loop and appending to the vector what I needed.

Thankfully, the compiler will aid you in telling you where mutable and immutable borrows happen so you scope data properly; sometimes it will tell you to issue annotations called, [lifetimes](https://doc.rust-lang.org/book/ch10-03-lifetime-syntax.html) which were needed sometimes when needing to explicitly describe how long some data needs to stay in memory.

### Cargo

Cargo is Rust's package manager and is a powerful tool. Cargo can check your code, run and build your program, run tests, and much more. I found it fairly easy to work with and manage dependencies. A Rust project is configured through a `Cargo.toml` file. To install a library all you need to do is add `mylib = 1.0.0` under `[dependencies]` and run `cargo check`. All rust *crates* can be found at [crates.io](https://crates.io/); it's an excellent ecosystem and most libraries I used were well documented and supported. I additionally made use of [cargo-make](https://sagiegurari.github.io/cargo-make/), a build tool and task runner that I utilized to write intialization scripts (I'll cover more of this further in the frontend section).

## The Bridge to Elm

To actually render the GUI, I used a Rust library called [webview](https://github.com/Boscop/web-view), which renders HTML like a web browser and supports two-way bindings between Rust and JavaScript. If you've ever used Electron, it's extremely similar to using IPCs, which allow you to pass messages from the frontend to the backend and visa-versa. The cool thing about using Rust is the ability to send and receive type-safe JSON; something you can't get out of the box with Electron. 

Now, in the spirit of type-safety and reliablility, I opted in to using [Elm](https://elm-lang.org/) for the frontend. Elm is a typed, functional programming language. The Elm compiler is quite friendly and readable, aiding in preventing runtime-errors (none of those `Cannot read property -stuff- of undefined`!). Lately, I've been using a ton of [Ramda](https://ramdajs.com/) in JavaScript, as well as writing some [Elixir](https://elixir-lang.org/) from time to time. Thus, Elm was an excellent choice to satiate and improve my FP prowess. The learning curve wasn't too steep. It's lisp-like syntax was a bit off-putting at first, as I have never used a true lisp, but I eventually got the hang of it; understanding that every function in Elm is curried was key. The way to compose functions was to wrap an invocation in parentheses. So a function that operates on data that also needs some other operation looks something like:

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