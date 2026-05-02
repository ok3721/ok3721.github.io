---
   layout: post
   title: "Today I Learned how to override Rust crates"
   date:   2026-05-03 00:31:41 +0800
   categories: rust
   tags: rust winit alacritty
---

Today I Learned how to override a Rust project dependency, in order to use the local fork of a crate that's been published on crates.io.

## The problem
As I mentioned in [Trying out Neovim as a VScode user](https://ok3721.github.io/others/2026/04/05/trying-neovim.html), currently `neovide` and `alacritty` have a weird [glitch‌](https://github.com/alacritty/alacritty/issues/8634) that infinitely resizes when you drag one window to a second monitor, which in turn is a [bug](https://github.com/rust-windowing/winit/issues/4041) orginated from the upstream `winit` crate.

While this bug is fixed in `winit v0.31.0-beta.2`, this new version also introduces lots of API updates and it won't be merged to alacritty anytime soon‌ ([alacritty/pull/8750](https://github.com/alacritty/alacritty/pull/8750))

## The solution
As in Rust tradition, `cargo` also have wonderful  [document](https://doc.rust-lang.org/cargo/reference/overriding-dependencies.html) to learn the basics. The problem here is exactly the same case as in the tutorial, I followed the instruction, cloned `winit v0.30.9`, which is the version used in alacritty, and applied the fix in [commit 488c036](https://github.com/rust-windowing/winit/commit/488c036a05d418e13bbdcdc349e2db2f6b7f58e2). I use Windows 11, so the fix is as simple as ignore all the Win10 fix, and just use `suggested_rect` when the window is in another monitor with different DPI. After the fix, I tested it with an empty window, works great, next I cloned alacritty, added `[patch.crates-io]` to its cargo manifest, compiled the executable, and viola, my own `alacritty.exe` works great when dragged between two monitors, problem solved!

