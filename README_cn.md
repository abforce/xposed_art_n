### 简介

这个项目是AOSP 7.1.2的一个子模块 `art/`,自带xposed功能。也就是说，不需要用户root设备来安装Xposed。Xposed已经默认安装。

###  和rovo89的xposed差异

未修改的xposed有点像是一个patch，作用在已经编译好的固件上，重新编译很多已经编译好的 `dex`文件。但是我的这种份ART不会重新编译任何dex，我的ART在编译的时候就考虑到xposed，（比如 禁止内联函数和直接调用）。内联函数和直接调用大体上说是相似的，因为都采用相同的机制来hook方法。准确的说，我将rovo89的提交，当然这些提交是和hook相关的，移植到AOSP版本Android N上的ART

### 怎样编译一个内置支持xposed的固件？

 - 使用我的版本代替原来的`art/` 子模块
 - 使用修改的版本代替原来的`frameworks/base/cmds/app_process`
 - 将`XposedBridge.jar`拷贝到`system/framework` 从而构建出一个预先编译好的模块
 - 更新 `built/target/product/base.mk` ，将`libxposed_art` 和`XposedBridge`包含在主makefile编译规则文件中
 
 ### 在哪里找到 我的ART修改提交？
 
 去吧！事实上，为了简便，我将所有的提交规整到了一个提交，rovo89的提交也是规整到了一个提交 
 
 ### 查看ART提交的差异？

 在这里 https://github.com/abforce/xposed_art_n/commit/1d14337b858cabd184335804b178f16849186f89
 
 ### 注意
 
 在转化rovo89针对Android N的提交的过程中，`art_method-inl.h`中的`VisitRoots`方法被全部重写。所以，我不确定我的移植是否正确，我也只是黑天瞎开火，期望能误打误撞
 
 ### 有问题？
 
 参看 [issues](https://github.com/abforce/xposed_art_n/issues)
 
 Copy right 版权
 然而MIT没有包含版权文件！
