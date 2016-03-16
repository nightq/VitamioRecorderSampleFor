VCamera
===============

VCamera SDK Android版（短视频拍摄SDK）是炫一下（北京）科技有限公司官方推出的Android平台使用的软件开发工具包，为Android开发者提供简单、快捷的接口，帮助开发者实现Android平台上的短视频应用开发。


## 使用android studio编译

>####1.如果使用android studio 开发，在使用 muldex 并打开的情况下，由于vitamio 的jar是混效过的，所以会导致再次打包的时候混淆一个混淆过的jar包的错误：

> `java.io.IOException: Can't read [ /build/intermediates/transforms/jarMerging/aliyun/debug/jars/1/1f/combined.jar] (Can't process class [com/yixia/camera/demo/ui/record/helper/ThemeHelper.class] (Unknown verification type [10] in stack map frame))`

>####2.如下是我的解决方案：
>
> 1.  首先在 [《Proguard源码库》](https://sourceforge.net/projects/proguard/) 右下角 Tags 选择一个版本(eg. 5.2.1)的标签， 然后点击左边的 Download Snapshot 按钮进行下载这个版本的源码。
> 2.  解压放到您的android studio 的 sdk/tools 目录下并以 proguard5.2.1 命名，以便与sdk自带的proguard包区分。
> 3.  参考 [《修改proguard源码》](http://innodroid.com/blog/post/use-a-custom-proguard-build-with-gradle) 修改  tools/proguard5.2.1/src/ClassContacts.java 里面的 
<br />`public static final String ATTR_StackMapTable = "StackMapTable";`
<br />替换为：
<br />`public static final String ATTR_StackMapTable = "dummy";` 
<br />在 proguard5.2.1/buildscripts 目录下使用 [ant命令](http://ant.apache.org/) 编译 (如没有安装自寻在网上搜索安装).编译完成后会在 proguard5.2.1/lib 目录下生成 proguard.jar 等文件.
> 4.  需要在项目工程里面配置使用新版本的依赖和引用：
<br />在根目录的 build.gradle 里面添加：
<br /><pre><code class="language-text" data-lang="text">
buildscript {
    repositories {
        // 引用 proguard 包
        flatDir { dirs 'proguard' }
        jcenter()
    }
    dependencies {
        // 这里的 5.2.1 是根据你下载的版本号填写
        classpath 'proguard.io:proguard:5.2.1'
        classpath 'com.android.tools.build:gradle:2.0.0-beta5' 
    }
}</code></pre>

>####3.clear 您的工程。进行编译就行了。

建议
----------
不要将 tools/proguard5.2.1/lib/proguard.jar 直接放入 tools/proguard/lib 里面替换。因为可能 android studio版本不支持导致你在其他项目里使用到 proguard 的时候不能使用 5.2.1 的版本而也需要将上面 第四条的修改加入到你的其他项目。引起麻烦。

特性
------------

# 支持分段拍摄、回删
# 支持静态/动态水印、声音主题合成
# 支持FFmpeg命令行
# 支持ARMV7 CPU

如何使用
----------

请参考VCamera Android SDK用户手册_v1.x.pdf

授权
-------

个人免费，企业收费（商务sales@yixia.com，电话座机010-6482 8682）