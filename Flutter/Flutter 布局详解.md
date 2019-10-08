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

// TODO  https://github.com/yang7229693/flutter-study/blob/master/post/3.%20Flutter%20%E5%B8%83%E5%B1%80%E8%AF%A6%E8%A7%A3.md






