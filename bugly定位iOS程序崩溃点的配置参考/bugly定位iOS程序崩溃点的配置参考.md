# Intership\bugly定位iOS程序崩溃点的配置参考

## 首先是崩溃函数的编写

![](C:\Users\ranqinyuan.than\Desktop\Intership\bugly定位iOS程序崩溃点的配置参考\PictureQuote\QQ图片20200722172923.jpg)

- 在Xcode下新建一个**.m**文件然后将后缀改为**.mm**
- 将.mm文件导入unity\assets\Plugins\iOS目录下
- 选择一种你喜欢的方式（我用了Button点击事件）调用

![](C:\Users\ranqinyuan.than\Desktop\Intership\bugly定位iOS程序崩溃点的配置参考\PictureQuote\QQ截图20200722173214.png)

- 然后打包成Xcode工程，编译运行即可在iOS上触发崩溃

## 然后是Bugly的集成，接收崩溃消息

[参考链接1](https://bugly.qq.com/docs/user-guide/instruction-manual-plugin-unity/?v=20200622202242)

[参考链接2](https://bugly.qq.com/docs/user-guide/instruction-manual-ios/?v=20200622202242)

### 总体流程

#### 通用部分集成

**下载并导入Bugly Unity Plugin到Unity项目工程**

- 下载最新版本Bugly Unity Plugin，双击.unitypackage文件，导入Plugin的相关文件到Unity工程中。

  > 下载包目录结构说明
  >
  > - **bugly_plugin_\*.unitypackage** - Bugly Unity Plugin包, 提供C#异常捕获功能及原生SDK接口封装
  > - **BuglySDK** - Bugly原生SDK, Plugin包依赖的原生SDK
  > - **BuglyUnitySample** - Unity工程示例

双击**bugly_plugin_\*.unitypackage**文件，根据平台需求导入文件到Unity工程(如果你正在使用旧版本Plugin包，请务必先删除旧版本相关的文件）

> bugly_plugin_*.unitypackage目录结构说明
>
> - Assets/Plugins/BuglyPlugins - Plugin脚本
> - Assets/Plugins/BuglyPlugins/Android/libs - Android平台依赖的原生SDK(.jar)及NDK组件(.so)
> - Assets/Bugly.framework - iOS平台依赖的原生SDK静态库（需要单独下载iOS SD）

- 下载最新版本Bugly Unity Plugin，双击.unitypackage文件，导入Plugin的相关文件到您的Unity工程中。

> 下载包目录结构说明
>
> - **bugly_plugin_\*.unitypackage** - Bugly Unity Plugin包, 提供C#异常捕获功能及原生SDK接口封装
> - **BuglySDK** - Bugly原生SDK, Plugin包依赖的原生SDK
> - **BuglyUnitySample** - Unity工程示例

- 双击**bugly_plugin_\*.unitypackage**文件，根据平台需求导入文件到Unity工程(如果你正在使用旧版本Plugin包，请务必先删除旧版本相关的文件）

> bugly_plugin_*.unitypackage目录结构说明
>
> - Assets/Plugins/BuglyPlugins - Plugin脚本
> - Assets/Plugins/BuglyPlugins/Android/libs - Android平台依赖的原生SDK(.jar)及NDK组件(.so)
> - Assets/Bugly.framework - iOS平台依赖的原生SDK静态库**（需要单独下载iOS SDK，单独导入）**

#### 初始化Bugly

选择第一个或主场景(*Scene*)，在任意脚本文件(建议选择较早加载的脚本)中调用如下代码进行初始化。

**我是单独在一个脚本的Awake方法里面写了这段初始化**

```c#
    // 开启SDK的日志打印，发布版本请务必关闭
    BuglyAgent.ConfigDebugMode (true);
    // 注册日志回调，替换使用 'Application.RegisterLogCallback(Application.LogCallback)'注册日志回调的方式
    // BuglyAgent.RegisterLogCallback (CallbackDelegate.Instance.OnApplicationLogCallbackHandler);

    #if UNITY_IPHONE || UNITY_IOS
        BuglyAgent.InitWithAppId ("Your App ID");
    #elif UNITY_ANDROID
        BuglyAgent.InitWithAppId ("Your App ID");
    #endif

    // 如果你确认已在对应的iOS工程或Android工程中初始化SDK，那么在脚本中只需启动C#异常捕获上报功能即可
    BuglyAgent.EnableExceptionHandler ();
```

#### iOS部分的集成

**我选择了手动集成**

**修改导出的Xcode工程的编译配置**

切换到*Build Phases*选项卡，在Link Binary With Libraries栏目下添加如下依赖项：

> - **libz.dylib**或者**libz.tbd** - 用于对上报数据进行压缩
> - **Security.framework** - 用于存储keychain
> - **SystemConfiguration.framework** - 用于读取异常发生时的系统信息
> - **JavaScriptCore.framework** - 设置为Optional
> - **libc++.dylib**或者**libc++.tbd** - libc++库依赖

#### ※初始化iOS SDK

##### 导入头文件

在工程的`AppDelegate.m`文件导入头文件

> ```
> #import <Bugly/Bugly.h>
> ```
>
> **如果是`Swift`工程，请在对应`bridging-header.h`中导入**

##### 初始化Bugly

我选择的是OC语言

在工程`AppDelegate.m`的`application:didFinishLaunchingWithOptions:`方法中初始化：

- **Objective-C**

```objective-c
- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
    [Bugly startWithAppId:@"此处替换为你的AppId"];
    return YES;
}
```

- **Swift**

```swift
func application(application: UIApplication, didFinishLaunchingWithOptions launchOptions: [NSObject: AnyObject]?) -> Bool {
    Bugly.startWithAppId("此处替换为你的AppId")
    return true
}
```

***特别注意：*****AppDelegate.m文件**我在导出的Xcode工程中没有找到，通过搜索方法名的方式找到了**UnityAppController.mm**中存在相应的方法

##### 编译运行

至此，触发崩溃即可在bugly个人主页上收到崩溃消息

### 需要特别注意的点：

- bugly_unity.unitypackage文件导入后，文件目录与参考链接**有所出入**，**需要手动将BuglySDK\iOS\Bugly.framework导入到unity\assets文件下**

  ![](C:\Users\ranqinyuan.than\Desktop\Intership\bugly定位iOS程序崩溃点的配置参考\PictureQuote\QQ截图20200722174627.png)

- Xcode工程这边，我选择了手动集成

  注意：参考链接1和2中**依赖库**相差了一个**JavaScriptCore.framework** ，我选择将其添加进依赖，**记得设置为Optional**

- 初始化iOS SDK过程中，搜索不到**AppDelegate.m文件**，在**UnityAppController.mm文件**中找到了相应的方法

## 最后是符号表的配置

有手动和自动配置两种方式

[参考链接](https://bugly.qq.com/docs/user-guide/symbol-configuration-ios/?v=20200622202242)

### 手动配置（↑自动配置传送门）

**注意：需要java运行环境，需要符号表工具和dSYM文件**

手动配置的流程如下：

- 下载最新版**[Bugly iOS符号表工具](https://bugly.qq.com/v2/sdk?id=15343657-638a-4569-a220-8689b090be65)**，其中工具包中包括：

  - 符号表工具JAR包（buglySymboliOS.jar）
  - Windows的脚本（buglySymboliOS.bat）
  - Shell脚本（buglySymboliOS.sh）
  - 默认符号表配置文件（settings.txt）
  - 符号表工具iOS版-使用指南

- 修改settings.txt文件配置

  ID为Bugly平台App ID

  Key为Bugly平台的App Key

  ![](C:\Users\ranqinyuan.than\Desktop\Intership\bugly定位iOS程序崩溃点的配置参考\PictureQuote\QQ图片20200722192239.jpg)

- 终端进入到符号表工具解压后的文件夹中
- 执行命令**java -jar buglySymboliOS.jar -i ”.dSYM的文件路径“（没有双引号）**
- 提取出来的符号表文件后缀为.zip会出现在.dSYM的上级目录中（我的直接上传了，如果没有上传可以手动上传一下）

### 注意：

#### 如何定位.dSYM文件？

一般情况下，项目编译完dSYM文件跟app文件在同一个目录下，下面以XCode作为IDE详细说明

1. 进入到Xcode已经通过编译的工程
2. 进入到左栏Product文件夹下
3. 右键xxx.app，”show in finder“

![](C:\Users\ranqinyuan.than\Desktop\Intership\bugly定位iOS程序崩溃点的配置参考\PictureQuote\QQ图片20200722193328.jpg)

### XCode编译后没有生成dSYM文件？

修改两处

一

![](C:\Users\ranqinyuan.than\Desktop\Intership\bugly定位iOS程序崩溃点的配置参考\PictureQuote\QQ图片20200722193715.jpg)

二

![](C:\Users\ranqinyuan.than\Desktop\Intership\bugly定位iOS程序崩溃点的配置参考\PictureQuote\QQ图片20200722193821.jpg)