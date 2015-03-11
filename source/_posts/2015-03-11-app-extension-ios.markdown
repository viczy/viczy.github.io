---
layout: post
title: "App-Extension-iOS"
date: 2015-03-11 08:28:44 +0800
comments: true
categories: 
---

##Extension环境
* iOS8+

##Extension概述
Extension让app之间的数据交互成为可能。用户可以在app中使用其他应用提供的功能，而无需离开当前的应用。

在iOS 8系统之前，每一个app在物理上都是彼此独立的，app之间不能互访彼此的私有数据。

而在引入扩展之后，其他app可以与扩展进行数据交换。基于安全和性能的考虑，每一个扩展运行在一个单独的进程中，它拥有自己的bundle， bundle后缀名是.appex。

iOS 8系统有6个支持扩展的系统区域，分别是Today、Share、Action、Photo Editing、Storage Provider、Custom keyboard。支持扩展的系统区域也被称为扩展点。

##Extension的生命周期
![lifecyle](images/App-Extensions-iOS/app_extensions_lifecycle.png)

extension的开始于用户通过host-app点击extension,`系统`启动Extension；终止于用户取消任务，或者任务执行结束，或者开启了一个长时后台任务时，系统会将其杀掉。
 
##Extension的通信
![communication](images/App-Extensions-iOS/simple_communication.png)

extension与host-app直接通信，而host-app与containing-app之间绝对不会通信。extension与containing不会通信但可以数据共享。如下图：
![Mou icon](images/App-Extensions-iOS/communication.png)

extension和containing-app可以共同读写一个被称为Shared resources的存储区域，这是通过App Groups实现。

最终host-app，extension，containing-app的三者关系如下图：

![detail](images/App-Extensions-iOS/detailed_communication.png)

##Extension类型

###Today Extension

通常被成为”组件”,Today Extension出现在通知中心的今日视点。这些小视图控制器包含着信息片段让用户一目了然。我们已经看到过苹果自带股票和天气等小”组件”(Widget)的形式。

![detail](images/App-Extensions-iOS/today.png)

###Share Extension
在iOS 8之前，用户只有Facebook,Twitter等有限的几个分享选项可以选择。如果希望将内容分享到Pinterest，开发者则需要一些额外的努力。在iOS 8中，开发者可以创建自定义的分享选项。

![detail](images/App-Extensions-iOS/share.png)

###Action Extension
action在所有支持的扩展点中扩展性最强的一个。它可以实现转换另一个app上下文中的内容。苹果在WWDC大会上演示了一个Bing翻译动作扩展，它可以将在Safari中选中的文本翻译成不同的语言。

![detail](images/App-Extensions-iOS/action.png)

###Photo Editing Extension
在iOS 8之前，如果你想为你的照片添加一个特殊的滤镜，你需要进入第三方app中，这个过程是相当繁琐的。在iOS 8中，你可以直接在Photos中使用第三方app，如Instagram，VSCO cam、Aviary提供的Photo Editing扩展完成对图片的编辑，而无需离开当前的app。

![detail](images/App-Extensions-iOS/photo.png)

###Document Provider Extension
Storage Provider让跨多个文件存储服务之间的管理变得更简单。类似Dropbox、Google Drive等存储提供商通过在iOS 8中提供一个Storage Provider扩展，app直接可以使用这些扩展检索和存储文件而不再需要创建不必要的拷贝。

![detail](images/App-Extensions-iOS/photo.png)


###Custom Keyboard Extension
苹果公司在2007年率先推出了触摸屏键盘，但一直没多大改进。在这一方面，Android则将键盘权限开放给了第三方开发者，所以出现了许多像Swype，SwiftKey,搜狗等优秀的键盘输入法。在iOS 8中，苹果终于将键盘权限开发给了第三方开发者，自定义键盘输入法可以让用户在整个系统范围内使用。

![detail](images/App-Extensions-iOS/keyboard.png)


##拓展
更多信息请关注苹果官方文档：[ExtensibilityPG](https://developer.apple.com/library/ios/documentation/General/Conceptual/ExtensibilityPG/ExtensibilityPG.pdf)


####参考资料
* <http://www.devtalking.com/articles/understand-how-an-extension-works/>
* <http://www.cocoachina.com/ios/20140721/9205.html>
* <https://github.com/ipader/SwiftGuide>