# Kotlin 学习笔记(三) 包与导入

------------------------------------------ 

这是一个Kotlin系列的教程，目的是为了使自己记忆和理解的更加深刻，将会添加对应的Java代码用于对比学习和更好的理解。  

------------------------------------------

## 目录
- [包](##包)
- [默认导入](##默认导入)
- [导入](##导入)

## 包

源文件通常以包声明开头:

```
package foo.bar

fun baz() {}

class Goo {}

// ……
```

源文件所有内容（无论是类还是函数）都包含在声明的包内。 所以上例中 ``baz()`` 的全名是 ``foo.bar.baz``、``Goo`` 的全名是 ``foo.bar.Goo``。

如果没有指明包，该文件的内容属于无名字的默认包。

## 默认导入

有多个包会默认导入到每个 Kotlin 文件中：  
- [kotlin.\*][链接1]    
- [kotlin.annotation.\*][链接2]  
- [kotlin.collections.\*][链接3]  
- [kotlin.comparisons.* （自 1.1 起）][链接4]  
- [kotlin.io.\*][链接5]  
- [kotlin.ranges.\*][链接6]  
- [kotlin.sequences.\*][链接7]  
- [kotlin.text.\*][链接8]

根据目标平台还会导入额外的包：

JVM:  

 - [java.lang.\*][链接9]  
 - [kotlin.jvm.\*][链接10]

JS:

 - [kotlin.js.\*][链接11]

## 导入

除了默认导入之外，每个文件可以包含它自己的导入指令。 导入语法在语法中讲述。

可以导入一个单独的名字，如.

```
import foo.Bar // 现在 Bar 可以不用限定符访问
```

也可以导入一个作用域下的所有内容（包、类、对象等）:

```
import foo.* // “foo”中的一切都可访问
```

如果出现名字冲突，可以使用 **as** 关键字在本地重命名冲突项来消歧义：

```
import foo.Bar // Bar 可访问
import bar.Bar as bBar // bBar 代表“bar.Bar”
```

关键字 **import** 并不仅限于导入类；也可用它来导入其他声明：

顶层函数及属性；
在对象声明中声明的函数和属性;
枚举常量。
与 Java 不同，Kotlin 没有单独的``“import static”``语法； 所有这些声明都用 ``import`` 关键字导入。

顶层声明的可见性
如果顶层声明是 **private** 的，它是声明它的文件所私有的（参见 可见性修饰符）。

- QQ邮箱：**1050629507@qq.com** 
- 上一篇：[Kotlin 学习笔记(二) 基本类型][基本类型]  
- 下一篇：[Kotlin 学习笔记(四) 控制流][控制流]   
- 参考文档：[Kotlin 语言中文站][语言中文站] 

 
 
[基本类型]:https://www.jianshu.com/p/9dd5b545f47b    
[控制流]:https://www.jianshu.com/p/e4932f8f8079 
[语言中文站]:https://www.kotlincn.net/  

[链接1]:https://kotlinlang.org/api/latest/jvm/stdlib/kotlin/index.html  
[链接2]:https://kotlinlang.org/api/latest/jvm/stdlib/kotlin.annotation/index.html    
[链接3]:https://kotlinlang.org/api/latest/jvm/stdlib/kotlin.collections/index.html
[链接4]:https://kotlinlang.org/api/latest/jvm/stdlib/kotlin.comparisons/index.html    
[链接5]:https://kotlinlang.org/api/latest/jvm/stdlib/kotlin.io/index.html    
[链接6]:https://kotlinlang.org/api/latest/jvm/stdlib/kotlin.ranges/index.html    
[链接7]:https://kotlinlang.org/api/latest/jvm/stdlib/kotlin.sequences/index.html    
[链接8]:https://kotlinlang.org/api/latest/jvm/stdlib/kotlin.text/index.html   
[链接9]:https://kotlinlang.org/api/latest/jvm/stdlib/java.lang/index.html 
[链接10]:https://kotlinlang.org/api/latest/jvm/stdlib/kotlin.jvm/index.html    
[链接11]:https://kotlinlang.org/api/latest/jvm/stdlib/kotlin.js/index.html
