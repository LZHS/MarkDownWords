# Kotlin 学习笔记(一) Kotlin初识
------------------
这是一个Kotlin系列的教程，目的是为了使自己记忆和理解的更加深刻，将会添加对应的Java代码用于对比学习和更好的理解。  


---------------

### 目录  
 
- [Kotlin与Java互转](#Kotlin与Java互转 )
- [HelloWorld](#HelloWorld) 
- [函数](#函数)  
- [表达式函数体](#表达式函数体)
- [变量](#变量)
- [可变变量和不可变变量](#可变变量和不可变变量)
- [字符串模版](#字符串模版)
- [类和属性](#类和属性)
- [属性](#属性)
- [定义访问器](#定义访问器)
- [枚举和When](#枚举和When)
- [循环](#循环)
- [Kotlin中的异常](#Kotlin中的异常)
 
# Kotlin与Java互转  
首先我们要知道  

- Kotlin和Java都是运行在JVM上，但是实际上JVM并不认识Java和Kotlin，因为它只和bytecode(即class文件)打交道。  
- 由于同一份bytecode反编译成Java和Kotlin文件是等价的所以讲Kotlin编译后的class文件反编译成Java，也是具有参考也研究价值的。  


以下基于IDEA或Android Studio具体方式是：  
> - **Kotlin 转 Java**  
>		1.  在AS中找到Tools>Kotlin>Show Kotlin Bytecode  
>		2. Decompile  
> - **Java 转 Kotlin**  
> 	打开要转化的文件  
>	- 方法一、 Ctrl + Shift + Alt + K  
>	- 方法二、 Code - Convert Java File To Kotlin File

----------------------
 

# HelloWorld
   
按照国际惯例学习一门新的语言先从 Hello ，world ！ 开始，我们最好还是按照Java的语法来翻译一下 （注意：使用Android Studio 会出现问题，建议使用**IDEA**。[问题分析][链接1]） 

Java 代码如下： 

```java
publilc static void main(String[] args){
	System.out.println("Hello,world");
} 
```

Kotlin代码如下：  

```kotlin
fun main(args: Array<String>){
	println("Hello , world")
}
```  

可以看到Kotlin中代码，让我们来简单推测一下  

- ``fun``关键字是用来声明一个函数  
- ``main``是方法名  
- ``args: Array<String>``表示参数，可以发现与Java中先类型后变量名相反，Kotlin中是先变量名，然后``:``,然后是类型声明。Kotlin中没有声明数组的特殊语法，而是用Array表示数组，有点类似集合的感觉；
- ``println``代替了``System.out.println``，这是Kotlin标准库给Java标准库提供了许多语法更简洁的包装  
- 最后一点不知道你有没有发现Kotlin 中省略的分号。

# 函数

对比Java的话你可能回想返回值在哪里？怎么会没有返回值？  

```kotlin
fun max(a: Int,b: Int): Int{
	return if(a>b) a else b
}
```  

- ``: Int``这里就出现，表示返回值是一个int类型，那为什么之前的``main``方法没有写呢？其实在上面的那个函数也是有返回值的，返回值为空，也就是``void``，在Kotlin中其实就是``: Unit``，而``: Unit``默认是可以省略的，所以就看不到返回值的申明  

同样，我们在来对比一下Java方法，代码如下：  

```java  
public static int max(int a,int b){
	if(a > b){
		return a;
	}else{
		return b;
	}
}
```  

对比发现方法体中的if的使用好像是有区别  
在Kotlin中，if是表达式，而不是语句。语句和表达式的区别在于，表达式有值，并且能作为另一个表达式的一部分使用；而语句总是包围着它的代码块中的顶层元素，并且没有自己的值。在Java中，所用的控制结构都是语句。而在Kotlin中除了循环（for，do,do/whlie）以外大多数控制结构都是表达式。  

# 表达式函数体

如果一个方法的函数体是由单个表达式构成的，可以用这个表达式作为完整的函数体，并且去掉花括号和return语句  

```kotlin
fun max(a: Int,b: Int) = if( a > b ) a else b
```  


> 在AS中通过Alt + Enter可以唤起操作，提供了在两种函数风格之间转换的方法： Convert to expression body (转换成表达式函数体) 和 Convert to block body (转换成代码块函数体)

也许你还注意到了此处的表达式函数也没有写返回类型，作为一门静态类型的语言，Kotlin不是要求每个表达式都应该在编译期间具有类型嘛？事实上，每个变量和表达式都要类型，每个函数都有返回类型，但是对表达式函数来说，编译器会分析作为函数体的表达式，并把它类型作为函数的返回类型，及时没有显示得写出来，这个分析通常被称之为类型推到。

# 变量

在Java中变量的声明是从类型开始的

```Java
final String str = "this is final string";
int a = 12 ;
```
刚才说了类型推断和类型声明，我们来看看Kotlin中是如何声明变量的  

```kotlin
val str: String = "this is a final string"
var a = 12
```

在Kotlin中是以关键字开始，然后是变量名称，最后可以加上类型（也可以省略）  
如上``: String``是可以省略的，通过 ``=``右边推导出左边变量的类型是String，就像``a``变量省略了类型

# 可变变量和不可变变量

声明变量的关键字有两个：  

- ``val``(来自value) ---- 不可变引用。在初始化之后不能再次复制，对应Java中final修饰符  
- ``var``(来自variable) ---- 可变引用。这种变量的值可以被改变，对应Java中的普通变量  

虽然``var``表示可变，并且如上面看到的也省略的类型，似乎和JS等脚本语言类似，可以直接复制另一种类型的值，比如这样：  

```kotlin 
var a = 12
a = "string" //错误的用法
```

但是实际上，这样做是错误的，即使``var``关键字允许变量改变自己的值，但它的类型缺失改变不了的。此处的变量在首次赋值的时候就确定了类型，这里的类型是``Int``，再次赋值``String``类型的值的时候就会提示错误，并且运行也会发生ClassCastException错误。  

注意，尽管``val``引用自身是不可变的，但是它指向的对象可能是可变的，例如：  

```kotlin
val languages = arrayList("Java")
languages.add("kotlin")
```

其实和Java中语法一致，final定义了一个集合，集合中的数据是可变的。  

# 字符串模版

```kotlin
val name = "Kotlin"
println("Hello,$name!")
```

这个是Kotlin中的新特性，在代码中，你申明了一个变量``name``，并且在后面的字符串字面值中使用了它，和许多的脚本语言一样，Kotlin让你可以在字符串字面值中引用局部变量，只需要在变量名称前面加上字符``$``，这等价于Java中的字符串链接``"Hello，" +  name + "!"``  
通过转化成Java代码，我们可以看到这两句代码其实是这样的：  

```kotlin
String name = "Kotlin";
String var3 = "Hello," + name + "!";
System.out.println(var3);
```

当然，表达式会进行静态检查，如果你试着引用一个不存在的变量，代码根本不会编译  
如果要在字符串中使用``$``，你需要对它转义：``println("\$x")``会打印出``$x``,并不会把``x``解释成变量的引用。  
还可以引用更为复杂的表达式，只需要把表达式用花括号括起来：  

```kotlin
println("1 + 2 = ${1 + 2 }")
```

还可以在双引号中直接嵌套双引号，只要它们在某个表达式的范围内（即花括号内）  

```kotlin
val a = 12
println("a ${if (a >= 10) "大于等于10" else "小于等于10"}”）
```

# 类和属性

先来看一个简单的JavaBean类Person,只设置了一个属性：name

```java  
public class Person {
    private final String name;

    public Person(String name) {
        this.name = name;
    }

    public String getName() {
        return name;
    }
} 
```  


在Java中，构造方法的方法体常常包含完全重复的代码：它吧参数赋值给有着相同名称的字段。在Kotlin中，这种逻辑不用这么多的样板代码就可以表达  
使用Convert Java File to Kotlin File 将这个对象转化成Kotlin  

```kotlin
class Person(val name: String)
```

这种只有数据没有其他代码的类通常被叫做值对象，许多语言都提供简明的语法来声明他们。  
注意从Java到Kotlin的转化过程中，``public``修饰符消失了，在Kotlin中默认的是``public``，所以可以省略它。

# 属性

类的概念就是把数据和处理数据的代码封装成一个单一的实体。在Java中，数据存储在字段中，通常还是私有的。如果想让类的使用者访问到数据，得提供访问器方法：一个getter，可能还有一个setter。在Person类中你已经看到了访问器的例子。setter还可以包含额外的逻辑，包括汗蒸传给它的值、发送关于变化的通知等。
在Java中，字段和其访问器的组合常常被叫做属性，在Kotlin中，属性时头等的语言特性，完全代替了字段和访问器的方法。在类中声明一个属性和声明一个变量一样：使用val和var关键字。声明成val的属性是只读的，而var属性是可变的。

```kotlin
class Person(
        val name: String //只读属性，生成一个字段和一个简单的getter
        var isMarried: Boolean //可写属性：生成一个字段、一个getter、一个setter
)
```

看看转换成Java的代码可能更清晰一点：

```Java
public final class Person {
   @NotNull
   private final String name;
   private boolean isMarried;

   @NotNull
   public final String getName() {
      return this.name;
   }

   public final boolean isMarried() {
      return this.isMarried;
   }

   public final void setMarried(boolean var1) {
      this.isMarried = var1;
   }

   public Person(@NotNull String name, boolean isMarried) {
      super();
      Intrinsics.checkParameterIsNotNull(name, "name");
      this.name = name;
      this.isMarried = isMarried;
   }
}
```

简单的说就是平时我们用代码模板生成的bean，在Kotlin中连模板都不需要使用了，编译时会自动生成对应的代码。
在Java中使用应该比较熟悉了，是这个是这样的

```java
Person person = new Person("LZHS", false);
System.out.println(person.getName());
System.out.println(person.isMarried());
```

生成的**getter**和**setter**方法都是在属性名称前加上**get**和**set**前缀作为方法名，但是有一种例外，如果属性时以**is**开头，**getter**不会增加前缀，而它的**setter**名称中**is**会被替换成**set**。所以你调用的将是``isMarried()``。
而在Kotlin中使用是这样的：

```kotlin
val person = Person("LZHS", false)     //调用构造方法不需要关键字new
println(person.name)    //可以直接访问属性，但调用的时getter
println(person.isMarried)
```

在Kotlin中可以直接引用属性，不在需要调用**getter**。逻辑没有变化，但代码更简洁了。可变属性的**setter**也是这样：  
在Java中，使用``person.setMarried(false)``来表示赋值，而在Kotlin中，可以这样写：``person.isMarried = false ``。  

# 定义访问器

如果**getter**和**setter**方法中需要额外的逻辑，可以通过自定义访问器的方式实现。例如现在有这样一个需求：声明一个矩形，它能判断自己是否是一个正方形。不需要一个单独的字段来存储这个信息，因为可以随时通过检查矩形的长宽是否相等来判断：

```kotlin
class Rectangle(val height: Int, val width: Int) {
    val isSquare: Boolean
        get() {//声明属性的getter
            return height == width
        }
}
```

属性``isSquare``不需要字段来保存它的值，它只有一个自定义实现的**getter**，它的值是每次访问属性的时候计算出来的。还记得之前的表达式函数体吗？此处也可以转成表达式体函数：``get() = height == width``。
同样的看下转换成Java代码更好理解：

```Java
public final class Rectangle {
   private final int height;
   private final int width;

   public final boolean isSquare() {
      return this.height == this.width;
   }

   public final int getHeight() {
      return this.height;
   }

   public final int getWidth() {
      return this.width;
   }

   public Rectangle(int height, int width) {
      this.height = height;
      this.width = width;
   }
}
```

# Kotlin目录和包
 
与Java类似，每个Kotlin文件都能以一天``package``语句开头，而文件中定义的所有声明（类、函数以及属性）都会被放到这个包中。如果其他文件中定义的声明也有相同的包，这个文件可以直接使用它们，如果包不相同，则需要导入它们。和Java一样，导入语句放在文件的最前面使用关键字``import``:

```kotlin
package lzhs.com

import java.util.Random
import lzhs.com.kotlin.Person
```

Java 中的包和导入声明：  

```java 
package lzhs.com;

import java.util.Random;
import lzhs.com.kotlin.Person;
```

仅仅省略了``;``还有点不同的是，Kotlin中不区分导入的是类还是函数（Kotlin中的函数可以单独存在的，不一定要声明在类中）例如：

```kotlin
package lzhs.com.kotlin

import java.util.*

fun createRandom() = Random().nextInt(100)
```

调动

```kotlin
import lzhs.com.kotlin.createRandom

fun  main(args: Array<String>){
    println(createRandom())
}
```

``lzhs.com.kotlin``是包名，``createRandom``是方法名，直接定义在Kotlin文件的顶层函数。
在Java中，要把类放在和包结构相匹配的文件与目录结构中。而在Kotlin中包层级机构不需要遵循目录层级结构，但是不管怎样，遵循Java的目录布局更根据包结构把源码文件放到对应的目录中是个更好的选择，避免一些不期而遇的错误


# 枚举和When

## 声明枚举
Kotlin中声明枚举：

```
enum class Color {
    RED, ORANGE, YELLOW, GREEN, BLUE
}
```

而Java中枚举的声明：

```
enum Color {
    RED, ORANGE, YELLOW, GREEN, BLUE
}
```

这是极少数Kotlin声明比Java使用了更多关键字的例子（多了**class**关键字）。Kotlin中，**enum**是一个软关键字，只有当它出现在**class**前面是才有特殊的意义，在其他地方可以把它当做普通的名称使用，与此不同的是，**class**任然是一个关键字，要继续使用名称**clazz**和**aClass**来声明变量。
和Java一样，枚举并不是值得列表，可以给枚举类声明属性和方法：

```
enum class Color(val r: Int, val g: Int, val b: Int) {

    RED(255, 0, 0), ORANGE(255, 165, 0),
    YELLOW(255, 255, 0), GREEN(0, 255, 255),
    BLUE(0, 0, 255);

    fun rgb() = (r * 256 + g) * 256 + b
}
```


枚举常量用的声明构造的方法和属性的语法与之前你看到的常规类一样。当你声明每个枚举常量的时候，必须提供该常量的属性值。注意这个向你展示了Kotlin语法中唯一必须使用分号（**;**）的地方：  
如果要在枚举类中定义任何方法，就要使用分号把枚举常量列表和方法定义分开。

## 使用**When**处理枚举类

对于Java，通常使用**switch**来匹配枚举，例如这样：

```
public String getColorStr(Color color) {
        String str = null;
        switch (color) {
            case RED:
                str = "red";
                break;
            case BLUE:
                str = "blue";
                break;
            case GREEN:
                str = "green";
                break;
            case ORANGE:
                str = "orange";
                break;
            case YELLOW:
                str = "yellow";
                break;
        }
        return str;
    }
```

而Kotlin中没有**switch**，取而代之的是**when**。和**if**相似，**when**是一个有返回值的表达式，因此我们写一个直接返回**when**表达式的表达式体函数:

```
fun getColorStr(color: Color) =
        when (color) {
            Color.RED -> "red"
            Color.ORANGE -> "orange"
            Color.YELLOW -> "yellow"
            Color.GREEN -> "green"
            Color.BLUE -> "blue"
        }
```
 
调用方法``println(getColorStr(Color.RED))``  
上面的代码根据传进来的``color``值找到对应的分支。和Java不一样，你不需要在每个分支都写上``break``语句（在Java中遗漏``break``通常会导致**bug**）。如果匹配成功，只有对应的分支会执行，也可以把多个值合并到同一个分支，只需要逗号（``,``）隔开这些值。

```
fun getColorStr(color: Color) =
        when (color) {
            Color.RED, Color.ORANGE, Color.YELLOW -> "yellow"
            Color.GREEN -> "neutral"
            Color.BLUE -> "cold"
        }
```

如果觉得写了太多的``Color``，可以通过导入的方式省略：

```
import com.huburt.other.Color //导入类
import com.huburt.other.Color.* //导入枚举常量

fun getColorStr(color: Color) =
        when (color) {
            RED, ORANGE, YELLOW -> "yellow" //直接使用常量名称
            GREEN -> "neutral"
            BLUE -> "cold"
        }
```

## 在**When**结构中使用任意对象

Kotlin中的**when**结构比Java中**switch**强大的多。**switch**要求必须使用常量（枚举常量、字符串或者数字字面值）作为分支条件。而**when**允许使用任何对象。我们使用这种特性来写一个函数来混合两种颜色：

```
fun mix(c1: Color, c2: Color) {
    when (setOf(c1, c2)) {
        setOf(Color.RED, Color.YELLOW) -> Color.ORANGE
        setOf(Color.YELLOW, Color.BLUE) -> Color.GREEN
        else -> throw Exception("Dirty color")
    }
}
```

``setOf``是Kotlin标准函数库中一个方法，用于创建Set集合（无序的）。
**when**表达式把``setOf(c1, c2)``生成的**set**集合依次和所有的分支匹配，直到某个分支满足条件，执行对应的代码（返回混合后颜色值或者抛出异常）。
能使用任何表达式作为**when**的分支条件，很多情况下会让你的代码既简洁又漂亮。

## 使用不带参数的When

你可能意识到上面的例子效率多少有些低。没此调用这个函数的时候它都会创建一些**Set**实例，仅仅是用来检查两种给定的颜色是否和另外两种颜色匹配。一般这不是什么大问题，但是如果这个函数调用很频繁，它就非常值得用另一种方式重写。来避免创建额外的垃圾对象。

```
fun mixOptimized(c1: Color, c2: Color) =
        when {
            (c1 == Color.RED && c2 == Color.YELLOW) ||
                    (c1 == Color.YELLOW && c2 == Color.RED) -> Color.ORANGE

            (c1 == Color.BLUE && c2 == Color.YELLOW) ||
                    (c1 == Color.YELLOW && c2 == Color.BLUE) -> Color.GREEN
            
            else -> throw Exception("Dirty color")
        }
```

如果没有给**when**表达式提供参数，分支条件就是任意的布尔表达式。``mixOptimized``方法和上面那个例子做了一模一样的事情，这种写法不会穿件额外的对象。

## 智能转换

在Java中经常会有这样一种情形：用父类申明引用一个子类对象，当要使用子类的某个方式时，需要先判断是否是哪个子类，如果是的话在强转成子类对象，调用子类的方法，用代码的话就是如下的情况：

```
class Animal {

}

class Dog extends Animal {
    public void dig() {
        System.out.println("dog digging");
    }
}

Animal a = new Dog();
if (a instanceof Dog) {
     ((Dog) a).dig();
}
```

在Kotlin中，编译器会帮你完成强转的工作。如果你检查过一个变量是某种类型，后面就不需要转换它，就可以把它当做你检查过的类型使用（调用方法等），这就是智能转换。

```
val d = Animal()
if (d is Dog) {
    d.dig()
}
```

这里**is**是检查一个变量是否是某种类型（某个类的实例），相当于Java中的**instanceof**。可以看到d变量是一个``Animal``对象，通过is判断是``Dog``后，无需强转就能调用``Dog``的方法。
智能转换只在变量经过is检查且且之后不再发生变化的情况下有效。当你对一个类的属性进行智能转换的时候，这个属性必须是一个val属性，而且不能有自定义的访问器。否则，每次对属性的访问是否都能返回相同的值将无从验证。

在Kotlin中用**as**关键字来显示转换类型（强转）：

```
val d = Animal()
val dog = d as Dog

``` 


## 用When代替If

Kotlin和Java中**if**有什么不同，之前已经提到过了。如**if**表达式用在适用Java三元运算符的上下文中：  
``if (a > b) a else b （Kotlin）和a > b ? a : b``  
（Java）效果一样。Kotlin没有三元运算符，因为**if**表达式有返回值，这一点和Java不同。
对于较少的判断分支用**if**没有问题，但是较多的判断分支则用**when**是更好的选择，有相同的作用，并且都是表达式，都有返回值。

## 代码块作为If和When的分支

上面的例子满足条件的分支执行只有一行代码，但如果某个分支中代码不止一行还如何处理那？当然是把省略的{}加上作为代码块：

```
val a = 1
val b = 2
var max = if (a > b) {
   println(a)
   a
} else b

var max2 = when {
   a > b -> {
     println(a)
     a
  }
  else -> b
}
```

代码块中最后一个表达式就是结果，也就是返回值。
对比Java的代码：

```
int a = 1;
int b = 2;
int max;
if (a > b) {
   System.out.println(a);
   max = a;
} else {
    max = b;
}
```

无法使用switch少了赋值操作，并且when的使用在多条件的情况下也更方便。 


# 循环

## While循环

Kotlin中while和do-while循环与Java完全一致，这里不再过多叙述


## 迭代数字：区间和数列

Kotlin中有区间的概念，区间本质上就是两个值之间的间隔，这两个值通常是数字：一个起始值，一个结束值，使用..运算符来表示区间：

```
val oneToOne = 1 .. 10
```

注意Kotlin的区间是包含的或者闭合的，意味着第二个值始终是区间的一部分。如果不想包含最后那个数，可以使用函数**until**创建这个区间：``val x = 1 until 10`` ，等同于``val x = 1 .. 9``

你能用整数区间做的最基本的事情就是循环迭代其中所有的值。如果你能迭代区间中所有的值，这样的区间被称作数列。
我们用整数迭代来玩**Fizz-Buzz**游戏。游戏玩家轮流递增计数，遇到能被3整除的数字就用单词fizz代替，遇到能被5整除的数字则用单词**buzz**代替，如果一个数字是3和5的公倍数，你得说**FizzBuzz**。

```
fun fizzBuzz(i: Int) = when {
    i % 15 == 0 -> "FizzBuzz"
    i % 5 == 0 -> "Buzz"
    i % 3 == 0 -> "Fizz"
    else -> "$i"
}

fun play() {
    for (i in 1..100) {
        print(fizzBuzz(i))
    }
}
```

Kotlin中for循环仅以唯一一种形式存在，其写法：  
``for <item> in <elements>``。
区间``1 .. 100`` 也就是``<elements>``，因此上面这个例子遍历了这个数列，并调用``fizzBuzz``方法。
假设想把游戏变得复杂一点，那我们可以从100开始倒着计数，并且只计偶数。

```
for (i in 100 downTo 1 step 2) {
     print(fizzBuzz(i))
}
```

这里``100 downTo 1``是递减的数列（默认步长是1），并且设置步长step为2，表示每次减少2。

## 迭代map

我们用一个打印字符二进制表示的小程序作为例子。

```
    val binaryReps = TreeMap<Char, String>()//使用TreeMap让键排序
    for (c in 'A'..'F') {//使用字符区间迭代从A到F之间的字符
        val binary = Integer.toBinaryString(c.toInt())//吧ASCII码换成二进制
        binaryReps[c] = binary//根据键c把值存入map
    }
    for ((letter, binary) in binaryReps) {//迭代map，把键和值赋给两个变量
        println("$letter = $binary")
    }
...
```

语法不仅可以创建数字区间，还可以创建字符区间。这里使用它迭代从A到F的所有字符，包括F。
for循环允许展开迭代中集合的元素（map的键值对），把展开的结果存储到两个独立的变量中：letter是键，binary是值。  
map中可以根据键老访问和更新map的简明语法。使用``map[key]``读取值，并使用``map[key] = value``设置它们，而不需要地爱用**get**和**put**。这段``binaryReps[c] = binary``等价于Java中的``binaryReps.put(c, binary)``;

你还可以使用展开语法在迭代集合的同时跟踪当前项的下标。不需要创建一个单独的变量来存储下标并手动增加它：

```
    val list = arrayListOf("10", "11", "1001")
    for ((index, element) in list.withIndex()) {
        println("$index : $element")
    }
```

使用**in**检查集合和区间的成员
使用**in**运算符来检查一个值是否在区间中，或者它的逆运算**!in**来检查这个值是否不在区间中。下面展示了如何使用**in**来检查一个字符是否属于一个字符区间。

```
fun isLetter(c: Char) = c in 'a'..'z' || c in 'A'..'z'
fun isNotDigit(c: Char) = c !in '0'..'9'
```

这种检查字符是否是英文字符的技巧看起来很简单。在底层，没有什么特别处理，依然会检查字符的编码是否位于第一个字母编码和最后一个字母编码之间的某个位置``（a <= c && c <= z）``。但是这个逻辑被简洁地隐藏到了标准库中的区间类实现。  
**in**运算符合**!in**也适用于**when**表达式。

```
fun recognize(c: Char) = when (c) {
    in '0'..'9' -> "It's a digit!"
    in 'a'..'z', in 'A'..'z' -> "It's a letter!"
    else -> "I don't know..."
}
```

# Kotlin中的异常
Kotlin的异常处理语句基本形式与Java类似，除了不需要new关键字，并且**throw**结构是一个表达式，能作为另一个表达式的一部分使用。

```
 val  b = if (a > 0) a else throw Exception("description")
```


**try、catch、finally**
和Java一样，使用带有**catch**和**finally**子句的**try**结构来处理异常，下面这个例子从给定的文件中读取一行，尝试把它解析成一个数字，返回这个数字；或者当这一行不是一个有效数字时返回**null**。

```
fun readNumber(reader: BufferedReader): Int? {
    try {
        val line = reader.readLine()
        return Integer.parseInt(line)
    } catch (e: NumberFormatException) {
        return null
    } finally {
        reader.close()
    }
}
```

**Int?**表示值可能是**int**类型，也可能**null**，Kotlin独特的**null**机制，不带**?**标识的声明无法赋值**null**，在之后的文章中会具体介绍。

和Java最大的区别就是**throws**子句没有出现在代码中：  
如果用Java来写这个函数，你会显示地在函数声明的后写上``throws IOException``。你需要这样做的原因是**IOException**是一个受检异常。在Java中，这种异常必须显示地处理。必须申明你的函数能抛出的所有受检异常。如果调用另外一个函数，需要处理这个函数的受检异常，或者声明你的函数也能抛出这些异常。  
和其他许多现在JVM语言一样，Kotlin并不区分受检异常和未受检异常。不用指定函数抛出的异常，而且可以处理也可以不处理异常。这种设计是基于Java中使用异常实践做出的决定。经验显示这些Java规则常常导致许多毫无意义的重新抛出或者忽略异常的代码，而且这些规则不能总是保护你免受可能发生的错误。

## try作为表达式

Kotlin中**try**关键字就像**if**和**when**一样，引入了一个表达式，可以把它的值赋给一个变量。例如上面这个例子也可以这样写：

```
fun readNumber(reader: BufferedReader): Int? =
        try {
            val line = reader.readLine()
            Integer.parseInt(line)
        } catch (e: NumberFormatException) {
            null
        } finally {
            reader.close()
        }
```

如果一个**try**代码块执行一切正常，代码块中最后一个表达式就是结果。如果捕获到了一个异常，相应的**catch**代码块中最后一个表达式就是结果。

 
- QQ邮箱：**1050629507@qq.com**  
- 下一篇：[Kotlin 学习笔记(二) Kotlin基础](https://www.jianshu.com/p/9dd5b545f47b)   
- 参考文档：  
 1. [Kotlin 语言中文站][链接2]  
 2. [https://www.jianshu.com/p/df78b7c4b138](https://www.jianshu.com/p/df78b7c4b138)



[链接1]:https://blog.csdn.net/yangzongbin/article/details/78394621  
[链接2]:https://www.kotlincn.net/
