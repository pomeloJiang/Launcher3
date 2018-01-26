# Launcher3
将MTK提供的Android8.1 Launcher3源码导入至Android Studio编译运行

最近开始做Android 8.1的项目，Launcher3相对于 7.0 改动比较大。将Launcher3导入至Android Studio方便调试。



参考网上的一篇文章：https://www.jianshu.com/p/28b1d205b4e6

修改protos目录下launcher_dump.proto

将原来  option java_package = "com.android.launcher3.model";

修改成 option java_package = "com.android.launcher3.model.nano";
为了能定位到LauncherDumpProto这个接口

---

# build.gradle
MTK提供的源码中加了测试框架

```diff
- final String SUPPORT_LIBS_VERSION = '26.0.0-SNAPSHOT'
+ final String SUPPORT_LIBS_VERSION = '27.0.1'
dependencies {
    compile "com.android.support:support-v4:${SUPPORT_LIBS_VERSION}"
    compile "com.android.support:support-dynamic-animation:${SUPPORT_LIBS_VERSION}"
    compile "com.android.support:recyclerview-v7:${SUPPORT_LIBS_VERSION}"
    compile "com.android.support:palette-v7:${SUPPORT_LIBS_VERSION}"
    compile 'com.google.protobuf.nano:protobuf-javanano:3.0.0-alpha-7'

    testCompile 'junit:junit:4.12'
    androidTestCompile "org.mockito:mockito-core:1.9.5"
    androidTestCompile 'com.google.dexmaker:dexmaker:1.2'
    androidTestCompile 'com.google.dexmaker:dexmaker-mockito:1.2'
    androidTestCompile 'com.android.support.test:runner:0.5'
    androidTestCompile 'com.android.support.test.uiautomator:uiautomator-v18:2.1.2'
    androidTestCompile "com.android.support:support-annotations:${SUPPORT_LIBS_VERSION}"
}
```

我用的Android Studio版本是3.0.1,在build的时候找不到 "26.0.0-SNAPSHOT"这个版本下的依赖包，于是我将 SUPPORT_LIBS_VERSION 改成了目前最新的的 27.0.1版本，重新编译仍会报错，按照错误提示将goole()仓库添加进去就好了。
```
repositories {
    mavenCentral()
    jcenter()
    google()
}
```


# 最后

如果喜欢原生干净的代码，也给大家提供个Google AOSP版的Launcher3地址：
```
git clone https://android.googlesource.com/platform/packages/apps/Launcher3
```

