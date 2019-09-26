# 语言特性

* Dart所有的东西都是对象，即使是数字numbers、函数function、null也都是对象，所有的对象都继承自Object类。

* Dart动态类型语言，尽量给变量定义一个类型，会更安全，没有显示定义类型的变量在Debug模式下类型回事dynamic（动态的）

* Dart在running之前解析你的所有代码，指定数据类型和编译是的常量，可以提高运行速度

* Dart中的类和接口是统一的，类即接口，你可以继承一个类，也可以实现一个类（接口）,自然也包含了良好的面向对象和并发编程的支持。

* Dart 提供了顶级函数（如：main（））

* Dart没有public、private protected 这些关键字，变量名以“_”开头意味着对它的lib是私有的。

* 没有初始化的变量都会被赋予默认值null。

* final的值只能被设定一次。const是一个编译时常量，可以通过const来创建常量值，```var c = const[];```这里的c还是一个变量，只是被赋值了一个常量值，它还是可以赋其它的值。实例变量可以是final但不能是const.

* 编程语言并不是孤立存在的，Dart也是这样，它有语言规范、虚拟机、类库和工具等组成：  

  * SDK : SDK 包含Dart VM 、 dart2js、Pub、库和工具。
  * Dartium: 内嵌Dart VM 的Chrominm,可以再浏览器中直接执行dart代码。
  * Dart2Js： 将Dart 代码编译为JavaScript的工具。 