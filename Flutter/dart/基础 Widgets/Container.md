
# Container 详解

> 本文主要介绍Flutter中非常常见Container，


## 1.简介

> A convenience widget that combines common painting,and sizing widgets.

Container 在Flutter中太常见了，官方给出的简介，是一个结合了绘制（painting）、定位（positioning）以及尺寸（sizing）widget 的widget。

我们可以得出几个信息，它是一个组合widget，内部有绘制widget、定位widget、尺寸widget。后续看到不少widget，都是通过一些更基础的widget组合而成的。

### 1.1组成
Container 的组成如下

* 最里面的是child元素；
* child元素首先会被padding包着；
* 然后添加额外的constraints 限制；
* 最后添加margin；

Container 的绘制过程：

* 首先绘制transform 效果
* 接着绘制decoration；
* 然后绘制child；
* 最后绘制foregroundDecoration

Container 自身尺寸的调节分两种情况：

* Container 在没有子节点（children）的时候，会师徒去标的足够大，除非constraints 是unbounded限制，在这种情况下，Container 会试图去变得足够小。
* 带子节点的Container，会根据子节点尺寸调节自身尺寸，但是Container构造器中如果包含了width、height以及constraints，则会按照构造器中的参数来进行尺寸调节。

### 1.2 布局行为
由于Container组合了一系列的widget，这些widget都有自己的布局行为，因此Container的布局行为有时候是比较复杂的。

一般情况下，Container会遵循如下的顺序去尝试布局：

* 对齐（alignment）；
* 调节自身尺寸适合子节点；
* 采用width、height以及constraints布局；
* 拓展自身去适应父节点；
* 调节自身到足够小。

进一步说

* 如果没有子节点、没有设置width、height以及constraints，并且父节点没有设置unbounded的限制，Container将会自身调整到足够小。
* 如果没有子节点、对齐方式（alignment）,但是提供了width、height或者constraints，那么Container会根据自身以及父节点的限制，将自身调节到足够小。
* 如果没有子节点、width、height、constraints以及alignment，但是父节点提供了bounded限制，那么Container会按照父节点的限制，将自身调整到足够大。
* 如果有alignment，父节点提供了unbounded限制，那么Container会将调节自身大小尺寸来包住child；
* 如果有alignment，并且父节点提供了bounded限制，那么Container会将自身调整的足够大（在父节点的范围内），然后将child 根据alignment调整位置
* 含有child，但是没有width、height、constraints以及alignment，Container会将父节点的Constraints，传递给child，并且根据child调整自身。

### 1.3 继承关系

```Object > Diagnosticable > DiagnostcableTree > Widget > StatelessWidget > Container```

从继承关系可以看出，Container是一个StatelessWidget.Container 并不是一个最基础的widget，它是由一系列的基础widget组合而成。


## 2.源码解析  

构造函数如下

```
    Container({
       Key key,
       this.alignment,
       this.padding,
       Color color,
       Decoration decaoration,
       this.foregroundDecoration,
       double width,
       double height,
       BoxConstraints constranints,
       this.margin,
       this.transform,
       this.child, 
    })

```
平时使用最多的，也就是padding、color、width、height、margin等属性。

### 2.1 属性解析

* **key：** Container唯一标识符，用于查找更新。  
* **alignment：** 控制child的对齐方式，如果container或者container父节点尺寸大于child的尺寸，这个属性设置会起作用呢，有很多种对齐方式。
* **padding：** decoration内部的空白区域，如果有child的话，child位于padding内部。padding与margin的不同之处在于，padding是包含在content内，而margin则是外部边界，设置点击事件的话，padding区域会响应，而margin区域不会响应。
* **color：** 用 来设置container背景色，如果foregroundDecoration设置话，可能会遮盖color效果。
* **decoration：** 绘制在child后面的装饰，设置了decoration的话，就不能设置color属性，否则会报错，此时应该在decoration中进行颜色的设置。
* **width：** container的宽度，设置为double.infinity可以强制在宽度上撑满，不设置，则根据child和父节点两者一起布局。
* **height:** container的高度，设置为double.infinity可以强制在高度上撑满。
* **constraints:** 添加到child上额外的约束条件。
* **margin：** 围绕在decoration和child之外的空白区域，不属于内容区域。
* **transform：** 设置container的变换矩阵，类型为Matrix4.
* **child:** container中的内容widget

