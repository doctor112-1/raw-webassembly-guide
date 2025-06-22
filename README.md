# Raw Webassembly Guide

<p align="center">
  <img src="/webassembly.png">
</p>

A guide to help understand WebAssembly and write some raw WebAssembly.

According to the official WebAssembly site, "WebAssembly (abbreviated Wasm) is a binary instruction format for a stack-based virtual machine. Wasm is designed as a portable compilation target for programming languages, enabling deployment on the web for client and server applications" (https://webassembly.org/). But what does that really mean?

Well, to put it simply, it's a language that compiled languages like Rust or C, can compile to. But why would you want to compile to WebAssembly?

The benefit of compiling to WebAssembly, is that your code can run almost anywhere. This means that code written in Rust, can run in places like the web! This is great since it allows you to make a lot of really cool stuff, and even compile existing applications to WebAssembly to allow them to run in the web.

Most of the time, WebAssembly is just a target that something compiles to, a magical file that (hopefully) works. But how does it work? I made this repo to write down what I learnt, and hopefully to teach others the magic behind WebAssembly.

<p align="center">
  <a href="/guide/table-of-contents.md">
    Get Started →
  </a>
</p>

<sub>Credits to webassembly.org for the original image</sub>  
<sub>Inspiration taken from https://github.com/hackclub/some-assembly-required</sub>
