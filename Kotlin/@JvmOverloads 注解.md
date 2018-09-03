# @JvmOverloads 注解  
在Kotlin中@JvmOverloads注解的作用就是：在有默认参数值的方法中使用@JvmOverloads注解，则Kotlin就会暴露多个重载方法。  
可能还是云里雾里，直接上代码，代码解释一切：  

```

fun f(a: String, b: Int = 0, c: String="abc"){
    ...
}

```  

相当于在Java中声明 

```
void f(String a, int b, String c){
}

```

默认参数没有起到任何作用。

但是如果使用的了@JvmOverloads注解：  

```
@JvmOverloads fun f(a: String, b: Int=0, c:String="abc"){
}

```

相当于在Java中声明了3个方法：

```
void f(String a)
void f(String a, int b)
void f(String a, int b, String c)
```

是不是很方便，再也不用写那么多重载方法了。

注：该注解也可用在构造方法和静态方法。 

```
class MyLayout: RelativeLayout {

   @JvmOverloads
   constructor(context:Context, attributeSet: AttributeSet? = null, defStyleAttr: Int = 0): super(context, attributeSet, defStyleAttr)
}

```

相当Java中的：

```
public class MyLayout extends RelativeLayout {

    public MyLayout(Context context) {
        this(context, null);
    }

    public MyLayout(Context context, AttributeSet attrs) {
        this(context, attrs, 0);
    }

    public MyLayout(Context context, AttributeSet attrs, int defStyleAttr) {
        super(context, attrs, defStyleAttr);
    }
} 
```


