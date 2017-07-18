### Intro 简介
This is `art/` submodule of AOSP 7.1.2 which brings Xposed functionality out-of-the-box. That's, not requiring users to root their devices to install Xposed. Xposed is installed by default.
这个项目是AOSP 7.1.2的一个子模块 `art/`,自带xposed功能。也就是说，不需要用户root设备来安装Xposed。Xposed已经默认安装。
### What's the difference? 和rovo89的xposed差异
Untouched Xposed is kinda a patch that's applied on already built firmwares and then recompiles lots of already compiled `dex` files. But this copy of ART doesn't *recompile* anything. It compiles with Xposed considerations in mind (e.g. disabling method inlining and direct call). This two are similar in sofar as both share the exactly same mechanism to hook methods. Actually I've ported rovo89's commits (of course those relating to hooking) to ART of AOSP version N.
未修改的xposed有点像是一个patch，作用在已经编译好的固件上，重新编译很多已经编译好的 `dex`文件。但是我的这种份ART不会重新编译任何dex，我的ART在编译的时候就考虑到xposed，（比如 禁止内联函数和直接调用）。内联函数和直接调用大体上说是相似的，因为都采用相同的机制来hook方法。准确的说，我将rovo89的提交，当然这些提交是和hook相关的，移植到AOSP版本Android N上的ART
### How to build a built-in Xposed enabled firmware? 怎样编译一个内置支持xposed的固件？
 - Replace original `art/` submodule with this copy. 使用我的版本代替原来的`art/` 子模块
 - Replace original `frameworks/base/cmds/app_process` with [the modified one](https://github.com/abforce/xposed_app_process).使用修改的版本代替原来的`frameworks/base/cmds/app_process`
 - Create a prebuilt module that copies `XposedBridge.jar` to `system/framework`. 将`XposedBridge.jar`拷贝到`system/framework` 从而构建出一个预先编译好的模块
 - Update `built/target/product/base.mk` to include `libxposed_art` and `XposedBridge` to the main makefile recipes.更新 `built/target/product/base.mk` ，将`libxposed_art` 和`XposedBridge`包含在主makefile编译规则文件中
 
 ### Where's ART commits? 在哪里找到 我的ART修改提交？
 Gone `:)`. Actually for sake of simplicity, I've flattened down all commits into a single commit, all rovo89's too.
去吧！事实上，为了简便，我将所有的提交规整到了一个提交，rovo89的提交也是规整到了一个提交 
 ### Looking for diff? 查看ART提交的差异？
 Here's. https://github.com/abforce/xposed_art_n/commit/1d14337b858cabd184335804b178f16849186f89
 在这里 https://github.com/abforce/xposed_art_n/commit/1d14337b858cabd184335804b178f16849186f89
 ### Notes 注意
 While translating rovo89's commits to Andorid N, `VisitRoots` method of `art_method-inl.h` had been changed completely, so I was just uncertain whether my port is correct or not. I was just shooting in the dark, to hopefully hit the target `:)`.
 在转化rovo89针对Android N的提交的过程中，`art_method-inl.h`中的`VisitRoots`方法被全部重写。所以，我不确定我的移植是否正确，我也只是黑天瞎开火，期望能误打误撞
 ### Issues? 有问题？
 See [issues](https://github.com/abforce/xposed_art_n/issues).
 参看 [issues](https://github.com/abforce/xposed_art_n/issues)
 ### Copy right 版权
 MIT. not included LICENSE file though!
然而MIT没有包含版权文件
