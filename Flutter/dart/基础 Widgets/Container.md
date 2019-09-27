
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

