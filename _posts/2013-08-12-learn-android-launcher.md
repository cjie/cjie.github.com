---
layout: post
title: "Android Launcher探索"
description: "Android Launcher相关技术学习和分析"
category: tech
tags: Android

---

### Android Launcher是神马？

Launcher俗称Home Screen，也就是我们启动Android系统后第一眼看到的应用程序。也许不完全准确，但我也把它叫做桌面程序。

Android太开放了，在Android上开发者可以很容易就开发一个自己的桌面程序，和系统自带的桌面地位一致，然后交给用户来选择使用哪一个。Android真是太开放了，简直是奔放，这在iOS中难以想象。

Launcher程序一般比较复杂，其地位也相当重要。入口嘛！互联网都讲究入口。Facebook之前也推出了其[Facebook Home][]应用，试图占领用户手机入口，但貌似不太成功，在Google Play上只获得2.5星的评价，悲剧。

现在OTT机顶盒越来越流行，各家机顶盒一般都有自己定制的UI界面，如果能做出一个体验较好的通用的Android机顶盒Launcher应用来，支持装在各家机顶盒和智能电视中，也许这个会有不错的市场吧！重点是有想象空间，参考百度19亿美金收购91，据说电视屏是目前唯一还没有被巨头垄断的入口了！

----------

### Hierarchyviewer UI分析工具

[Hierarchyviewer][]是Google提供的Android的UI分析工具。我理解，相当于Windows上的Spy++。功能强大，可以分析到各种应用程序的UI布局，生成树状图，还能生成漂亮的层次图呢！威武！对于想要分析和借鉴别家优秀的应用如何设计的是重大利好啊。

再一次，Android太奔放了，Android对于用户来说也许是好事，但是对于程序开发者来说也许就不见得了，丫的啥都能看到，程序也能很easy的反编译、资源文件啥的都能轻松提取到，那应用开发还有啥秘密可言？想要保护支持产权需要做更多的工作了。

在adt-bundle工具的`sdk/tools`目录中找到`hierarchyviewer.bat`文件，执行后就可以出现hierarchyviewer程序界面了。

![hierarchy_viewer.jpg](/assets/images/learn-android-launcher/hierarchy_viewer.jpg)

选择`com.miui.home/com.miui.home.launcher.Launcher`，则可显示出小米Launcher的布局结构：

![hierarchy_viewer_pixel_perfect_window_list](/assets/images/learn-android-launcher/hierarchy_viewer_pixel_perfect_window_list.jpg)

在运行hierarchyviewer.bat后，命令行中会显示：

> The standalone version of hieararchyviewer is deprecated.
> Please use Android Device Monitor (tools/monitor.bat) instead.

目前不建议单独运行此程序了，这些功能都被集成到Android Debug Monitor工具中，里面提供更全面更强大的工具集合。

再选择`com.youku.phone/com.youku.ui.activity.HomePageActivity`，则可显示出优酷手机版的布局结构：

![youku_phone_app_view_hierarchy_overview](/assets/images/learn-android-launcher/youku_phone_app_view_hierarchy_overview.jpg)

一般成熟应用的界面的view hierarchy是一个庞大复杂的树形结构，下面的截图只是冰山一角。

![tip_of_iceberg_of_view_hierarchy](/assets/images/learn-android-launcher/tip_of_iceberg_of_view_hierarchy.jpg)

当点击其中一个元素时，还能显示此元素的截图，对于分析界面布局来说非常方便。

![one_element_on_view_hierarchy](/assets/images/learn-android-launcher/one_element_on_view_hierarchy.jpg)

同时还能显示此元素在整体布局中的位置，不错！

![one_element_position](/assets/images/learn-android-launcher/one_element_position.jpg)


----------

**相关英语词汇**：

the tip of the iceberg 冰山一角

----------

**参考文献**：

- Android官方文档 Optimizing Your UI：<https://developer.android.com/tools/debugging/debugging-ui.html>

[Facebook Home]: <https://developer.android.com/tools/help/hierarchy-viewer.html>  "Facebook Home"
[Hierarchyviewer]: <https://developer.android.com/tools/help/hierarchy-viewer.html>  "Hierarchy Viewer"
