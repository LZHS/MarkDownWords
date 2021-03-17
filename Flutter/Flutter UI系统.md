# Flutter UI 系统

我们可以看到无论是 Android SDK 还是iOS的UIKit的指责都是相同的，它们只是语言载体和底层的系统不同而已，那么可不可以实现这么一个UI系统：可以使用同一种编程语言开发，然后针对不同操作系统API抽象一个对上接口一直，对下适配不同操作系统的中间层，然后在打包编译时在使用相应的中间层代码？如果可以做到，那么我们就可以使用同一套代码编写跨平台的应用了，而Flutter的原理正是如此，它提供一套Dart API，然后在底层通过Open GL 这种跨平台的绘制库（内部会调用操作系统API）实现了一套代码跨多端。由于Dart API 也是调用操作系统API，所以它的性能更接近原生。


>  注意，虽然Dart是先调用了Open GL，Open GL才会调用操作系统的API，但是这仍然是原生渲染，因为OpenGL只是操作系统API的一个封装库，它并不像WebView渲染那样需要JavaScript运行环境和CSS渲染器，所以不会有性能损失。


至此我们已经了解了Flutter UI系统和操作烯烃交互的这一部分原理，现在需要说一些它对应用开发者定义的开发标准。简单的概括来说就是：组合和相应式。我们要开发一个UI界面，需要通过组合其它Widget来实现，Flutter中，一切都是Widget，当UI要发生变化时，我们不去直接修改DOM，而是通过更新状态，让Flutter UI系统来根据新的状态来重新构建UI

## Widget 简介

我们知道在Flutter中几乎所有的对象都一个Widget。与原生开发中“控件”不同的是，Flutter中Widget的挂念更广泛，它不仅可以表示UI原色，也可以表示一些功能新的组件，例如：用于手势检测的 ```GestureDetector``` widget、用于APP猪蹄数据传递```Theme``` 等等，而原生开发中的控件通常是指UI原色，由于Flutter主要是用于构建用户界面的，所以在大多时候，读者可以认为Widget就是一个控件，不必纠结于概念。

### Widget与Element 
在Flutter中，Widget的功能是“描述一个UI元素的配置数据”，他就是说Widget其实并不是表示最终挥着在设备屏幕上的显示元素，而它只是描述显示元素的一个配置数据  。

实际上Flutter中真正代表屏幕上显示元素的类是```Element```，也就是说Widget只是描述Element的配置数据！**Widget只是UI原色的一个配置数据，并且一个Widget可以对应多个Element**，这是因为同一个Widget对象可以被添加到UI数的不同部分，而真正渲染时，UI树的每一个Element节点都会对应一个Widget对象，总结一下：

1. Widget实际上就是Element的配置数据，Widget树实际上是一个配置树，而真正的UI渲染树是由Element构成；不过，由于Element是通过Widget生成的，所以它们之间有对应关系，在大多数场景，我们可以宽泛的认为Widget树就是指UI控件树或UI渲染树。
2. 一个Widget对象可以对应多个Element对象。这很好理解，根据同一份配置（Widget），可以创建多个实例（Element）



## Element与BuildContext

### Element
