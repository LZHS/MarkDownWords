# MaterialApp

## 简介

> MaterialApp 代表了Material设计风格的应用。

* 包含许多Material设计风格所需要的一些基本控件

* 在WidgetApp中通过添加一些特定与Material设计风格的属性

## 基本用法

> 这里着重介绍MaterialApp 重要属性

* title： 在任务管理窗口中所显示的应用名字

* theme： 应用各种UI所使用的主题颜色

* color: 应用的主要颜色值（primary color），也就是安卓任务管理窗口中所显示的应用颜色

* home:引用默认所显示的界面Widget

* routes：应用的顶级导航表格，这个是多页面应用来控制页面跳转的，类似于网页的网址

* initialRoute: 第一个显示的路由名字，默认值为Window.defaultRouteName

* onGenerateRoute: 生成路由的回调函数，当导航的命名路由的时候时候，会使用这个来生成页面

* onLocaleChanged：当系统修改语言的时候，会触发这个回调

* navigatorObservers：医用Navigator的监听器

* debugShowMaterialGrid：是否显示Material design 基础布局网格，用来调试UI的工具

* showPerformanceOverlay： 显示性能标签

* showSemanticsDebugger、checkerboardRasterCacheImages、checkerboardOffscreenLayers