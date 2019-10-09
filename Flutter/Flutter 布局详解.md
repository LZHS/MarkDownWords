# Flutter 布局详解

> 本文主要介绍了Flutter布局相关的内容，对相关知识点进行梳理，并从实际例子触发，进一步讲解该如何去进行布局。

## 1.简介

在介绍Flutter布局之前，我们得先了解Flutter中的一些布局相关的特性。

### 1.1 边界约束（box constraints）

box constrainaints 有人也翻译为盒约束。箱约束，我个人觉得边界约束可能更为直观一些。  

Flutter中的边界约束，是指Widget可以按照指定限定条件，来决定自身如何布局空间。Flutter借鉴了很多React相关的东西，包括一些布局思想，但是它自身没有抽离布局样式，而是用不同Widget去实现不同的布局，将样式嵌入Widget中，用户可以像搭积木一样写布局，写法上跟React很像，只不过没了样式的设定。

这样做的好处，我觉得可能是为了统一的渲染，加入样式，会让布局复杂不少，在渲染层面会降低很多性能，因此，Flutter在大的方向上，加入了不同类型的布局Widget，在小的方向上，只给出了很少的定制化的东西，将布局限定在有限的范围内，在完成布局的同时，让整个渲染能够统一，加快了更新和渲染。

但是缺点同样明显，少了很多灵活性，不同的布局方式都被抽离出了Widget，大家需要了解的Widget会非常多，增加了学习成本。

### 1.2约束种类

在Flutter中，Widget是由其底层的RenderBox渲染，渲染边界的约束（Contraints）由父级给出，Widget在这些约束下调整自身尺寸。约束包括最小最大宽高，尺寸则是具体的宽高。

在Android 中，布局的宽高限定有三种，match_parent、wrap_content以及具体尺寸。在Flutter中也有这三种约束。

* 尽可能大的约束，例如：Center、ListView等；
* 跟随内容大小的约束，例如：Transform、Opacity 等；
* 指定尺寸的约束，例如：Image、Text等

但是，Flutter并没有把Widget处理的这么绝对，这些约束条件包含在Widget里，像Android可以再外面去指定，因此，一些Widget，例如Container，会根据参数的不同，约束条件也不同。Container默认是尽可能大的，但是给定尺寸的话，就会优先使用具体值。不同的Widget可能设置条件不同，其子Widget不同，约束条件也会不一样。Flutter将每种Widget限制在不同的约束范围里，实际布局的时候，还需要综合去考虑，

## 2、分类

按照约束条件来分类，很多Widget不太好区分开来，官方也是根据其子元素的个数来分类。

* 单个子元素（child）的布局，包括Container、Padding等
* 多个子元素（children）的布局，包括Row、Column等
* layout helper，例如ListView。Builder，在元素多的时候，用这种方式更加的高效，类似Android的RecyclerView,有自动的回收机制，这种严格意义上不能算是一个种类

### 2.1 优缺点

其中日常中的用多的，例如Container、Padding、Center、Align、Row、Column、Stack、ListView等

Flutter提供了接近30种不同的布局Widget，还是源于其对Widget的定位。对比其他移动端的开发平台，可以看出Flutter的布局Widget是巨多，这也是为什么Flutter现在学习曲线很长的一个原因。 

## 3.Widget详解

在Flutter中，我们平时自定义的Widget，一般都是继承自StatefulWidget或者StatelessWidget（并不只有这两种），这两种Widget是目前最常用的两种。如果一个空间自身状态不会去改变，创建了就直接显示，不会有色值、大小或者其他属性的变化，这种Widget一般都是继承自StatelessWidget,常见的有Container、ScrollView。如果一个控件需要动态的改变或者改变相应的一些状态，例如点击状态、色值、内容区域等，那么一般都是继承自StatefulWidget，常见的有CheckBox、APPBar、TabBar等，

### 3.1 Widget类

Widget类在Flutter中是非常重要的，继承自Widget类的有PreferredSizeWidget、ProxyWidget、RenderObjectWidget、StatefulWidget、StatelessWidget。我们日常使用的绝大部分Widget都是继承自Widget类。

查看Widget类源码，内部实现非常简单，构造函数如下：

```
const Widghet({this.key});
final Key key;
```
这个Key的作用，是用来控制在Widget数中替换Widget的时候使用的。其中Key类是Widget，Element以及SemanticsNode的唯一标识符，继承自Key的还有LocalKey以及GlobalKey。

### 3.2 State

在说到StatefulWidget之前，先说下State。State的作用有两点：、

1. 在Widget构建的时候可以被同步读取；
2. 在Widget的生命周期中可能会被改变；

#### 3.2.1 State 生命周期

State的生命周期有四种状态：
 
 * **created:** 当State对象被创建的时候，State.initState方法会被调用；
 * **initalized:** 当State对象被创建，但还没有准备构建时，State.didChangeDependencies在这个时候会被调用；
 * **ready:** 当State对象已经准备好构建，State.dispose没有被调用的时候；
 * **defunct:** State.dispose被调用后，State对象不能够被构建；



 ![图片](../images\687474703a2f2f776879736f6469616f2e636f6d2f696d616765732f53746174652532304c6966654379636c652e706e67.png)









