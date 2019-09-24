## Scaffold

> Scaffold 实现了基本的Material Design布局结构

在Material 设计中定义的单个界面上的各种布局元素，在Scaffold中都有支持，比如在左边栏的Drawers、snack bars、以及bottom sheets.

## 基本用法

Scaffold 有下面几个主要的属性

* appBar： 显示在界面顶部的一个AppBar

* body: 当前界面所显示的主要内容Widget

* floatingActionButton: Material设计中所定义的FAB，界面的主要功能按钮

* Drawer:侧边栏控件

* backgroundColor：内容的背景颜色，默认使用的是ThemeData.scaffoldBackgroundColor的值

* bottomNavigationBar:显示在页面底部的导航栏

* resizeToAvoidBottomPadding:控制界面内容body是否重新布局来避免底部覆盖了，比如当键盘显示的时候，重新布局避免被键盘盖住内容。默认值为true。