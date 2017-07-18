### Introduction
This is `art/` submodule of AOSP 7.1.2 which brings Xposed functionality out-of-the-box. That's, not requiring users to root their devices to install Xposed. Xposed is installed by default. Please note that you can't use this module on your existing ROMs. This ART should be placed in AOSP source tree, then building the whole ROM.

### What's the difference?
Original Xposed is kinda a patch that's applied on already built firmwares and then recompiles lots of already compiled `dex` files. But this copy of ART doesn't *recompile* anything. It on the other hand, compiles system `dex` files at the ROM build time with Xposed considerations in mind (e.g. disabling method inlining and direct call). This two are similar in sofar as both share the exactly same mechanism to hook methods. Actually I've ported rovo89's commits (of course those relating to hooking) to ART of AOSP version N.

### How to build a built-in Xposed enabled firmware?
 - Replace original `art/` submodule with this copy.
 - Replace original `frameworks/base/cmds/app_process` with [the modified one](https://github.com/abforce/xposed_app_process).
 - Create a prebuilt module that copies `XposedBridge.jar` to `system/framework`, or manually copy it and run `make snod` to include it in the `system.img`.
 - Update `build/target/product/base.mk` to include `libxposed_art` and `XposedBridge` to the main makefile recipes (optional).
 
 ### Where's ART commits?
 Gone `:)`. Actually for sake of simplicity, I've flattened down all commits into a single commit, all rovo89's too.
 
 ### Looking for diff?
 Here's. https://github.com/abforce/xposed_art_n/commit/1d14337b858cabd184335804b178f16849186f89
 
 ### Notes
 While translating rovo89's commits to Andorid N, `VisitRoots` method of `art_method-inl.h` had been changed completely, so I was just uncertain whether my port is correct or not. I was just shooting in the dark, to hopefully hit the target `:)`.
 
 ### Issues?
 See [issues](https://github.com/abforce/xposed_art_n/issues).
 
 ### Copy right
 MIT. not included LICENSE file though!
