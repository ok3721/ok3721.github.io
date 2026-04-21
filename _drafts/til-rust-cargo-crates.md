---
   layout: post
   title: "Trying out Neovim as a VScode user"
   date:   2026-04-05 20:34:41 +0800
   categories: rust
   tags: rust winit alacritty
---

Today I Learned how to override rust project dependency to use the local fork of a crate that's been published to crates.io.

## The problem
As I mentioned in [Trying out Neovim as a VScode user](https://ok3721.github.io/others/2026/04/05/trying-neovim.html), currently `neovide` and `alacritty` hav a weird [glitch‌](https://github.com/alacritty/alacritty/issues/8634) that infinitely resize when you drag one window to a second monitor, which in turn is a [bug](https://github.com/rust-windowing/winit/issues/4041) orginated from upstrem crate.
While this bug is fixed in [v0.31.0-beta.2](https://github.com/rust-windowing/winit/commit/488c036a05d418e13bbdcdc349e2db2f6b7f58e2), `winit-0.31.0-beta.2` introduces lots of API updates and it won't be merged to alacritty soon‌ ([alacritty/pull/8750](alacritty/pull/8750))

## The solution
Once again, as in Rust tradition, `cargo` also have wonderful  [document](https://doc.rust-lang.org/cargo/reference/overriding-dependencies.html) to learn the basics.
