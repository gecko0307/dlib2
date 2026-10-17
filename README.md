# dlib 2

Work-in-progress general purpose library for D, a successor of [dlib](https://github.com/gecko0307/dlib) based on [RTLD](https://github.com/gecko0307/rtld). It will feature a more carefully thought-out architecture and more low-level functions. Implementation of some features from dlib 1.x will be available soon.

## Background

Historically, dlib 1.x evolved along its own unique path, largely independent of the broader language ecosystem. The library has always prioritized maximum backward compatibility, which, over time, led to numerous compromises as new features were added, ultimately resulting in an overly convoluted codebase. Functions that rely on the garbage collector became intermixed with those that do not. Furthermore, dlib 1.x requires users to have a deep understanding of its specific architectural nuances. While some components work out of the box, others are often counterintuitive or require complex preparatory steps to execute correctly, making them cumbersome to use.

## Principles

dlib 2.0 will eliminate most of the shortcomings of the classic version of dlib, including:

- Dependency on Phobos. The library's core functionality has been moved to a separate package, RTLD, which can be compiled entirely independently of Phobos and druntime. Phobos will only be used in certain high-level components where no other approach is possible;
- A mix of GC-dependent and GC-independent code. Each individual component will be explicitly designated as either GC-based or GC-free.

## API Structure

dlib 2.0 will consist of several API layers:

- RTLD — a low-level runtime that replaces Phobos. It will support compilation for x86_64, AArch64, and, probably, WASM/WASI.
- dlib — an object-oriented layer providing higher-level functionality. It will serve as a unified abstract interface for system APIs (covering at least Unix and Windows) for features that can and should be implemented without D's garbage collector. This layer will maintain compatibility with the classic dlib 1.x API as much as possible.
- dlib2 — a new high-level API. This layer could, for instance, include built-in bindings to various popular C libraries. It could also feature a hardware-accelerated 2D canvas for graphics rendering, which could eventually serve as the foundation for a custom UI toolkit—thereby enabling the creation of applications with user interfaces using dlib.
