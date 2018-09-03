# RxJava 概述（一）
----------------------------

### 1、什么是函数式编程  
函数式编程是一种编程范式，是面向数学的抽象，将计算藐视为一种表达式求职，函数可以在任何地方定义，并且可以多函数进行组合。提现在RxJava上很明显的就是链式操作、操作符的应用。  

### 2、什么是响应式编程
响应式编程是一种面向数据流和变化传播的编程范式，数据更新是相关联的，举一个简单的例子：A= B + C ，A被赋值为B和C的值，紧接着B发生了变化，但是A却不会发生变化，但是如果是响应式编程，当B发生变化后，A 就会随之发生改变，体现在RxJava 上很明显的就是我们对数据流的操作以及当被观察者发生变化的时候，观察者随之发生变化。

### 3、什么是函数响应式编程  
把函数式编程里面的一套思路和响应式编程组合起来就是函数响应式编程。他们可以极大地简化项目，特别是处理嵌套回调的异步事件，复杂的列表过滤和变换或者事件相关的问题。

### 4、RxJava 概述 
* RxJava是一个函数库，让开发者可以利用可观察序列和LINQ风格查询操作符来编写异步和基于事件的程序  
* 开发者可以用Observables表示异步数据流，用LINQ操作符查询异步数据流，用Schedulers 参数化异步数据流的并发处理  
* Rx 可以这样定义 ： Rx = Observables + LINQ + Schedulers;

### 5、为何要使用RxJava  
代码间接：异步操作和Handler 、 AsyncTask 等，但是使用RxJava ,就算在多的异步操作，代码逻辑越来复杂，RxJava依然可以保持清晰的逻辑。  

举例：假如现在有这样一个绣球：界面上有一个自定义的视图imageCollectorView，它的作用是显示多张图片，并能使用addImage(Bitmap)  方法来任意增加显示图片。现在需要程序将一个给出的目录数组File[] folders 中每个目录下的PNG图片都加载出来并显示在imageCollectorView中。需要注意的是，由于读取图片中的这一过程较为耗时，需要放在后台执行，而图片的显示就必须在UI线程执行，我们分别展示非RxJava 的操作和RxJava的操作

```

///非RxJava：

new Thread() {
    @Override
    public void run() {
        super.run();
        for (File folder : folders) {
            File[] files = folder.listFiles();
            for (File file : files) {
                if (file.getName().endsWith(".png")) {
                    final Bitmap bitmap = getBitmapFromFile(file);
                    getActivity().runOnUiThread(new Runnable() {
                        @Override
                        public void run() {
                            imageCollectorView.addImage(bitmap);
                        }
                    });
                }
            }
        }
    }
}.start(); 

```


```

//RxJava：

Observable.from(folders)
    .flatMap(new Func1<File, Observable<File>>() {
        @Override
        public Observable<File> call(File file) {
            return Observable.from(file.listFiles());
        }
    })
    .filter(new Func1<File, Boolean>() {
        @Override
        public Boolean call(File file) {
            return file.getName().endsWith(".png");
        }
    })
    .map(new Func1<File, Bitmap>() {
        @Override
        public Bitmap call(File file) {
            return getBitmapFromFile(file);
        }
    })
    .subscribeOn(Schedulers.io())
    .observeOn(AndroidSchedulers.mainThread())
    .subscribe(new Action1<Bitmap>() {
        @Override
        public void call(Bitmap bitmap) {
            imageCollectorView.addImage(bitmap);
        }
    });
 

```
不难发现：RxJava 好久好在什么复杂的逻辑都能穿成一条线的简洁  

### 6、RxJava 的原理  
RxJava 的原理就是创建一个Observable对象老干活，然后使用各种操作符建立起来的链式操作，就如同流水线一样，想你想要处理的数据一步一步地加工成你想要的成品，然后发射给Subscriber处理

### 7、观察者模式（简单的说）
* 观察者模式需要解决的问题   
	* A 对象（观察者）对B对象（被观察值）的变化高度敏感，需要在B对象变化的一瞬间做出反应。
	 
* 现实生活中的观察与程序观察者模式的区别  
	* 生活着警察（观察者）抓小偷（被观察者），警察需要时时刻刻的盯着小偷作案，当小偷偷东西的那一刻，上前抓住小偷
	* 程序中的观察者模式：观察者不用时时刻刻的盯着被观察者，而是采用订阅的方式，观察者告诉被观察者你发生了变化通知我。

* 很常见的观察者模式  
	* Button（被观察者）与OnClickListener（观察者），通过setOnClickListener()方法达成订阅关系。
	* 采取这样被动的观察方式，即省去了反复检索状态的资源消耗，也能够得到最高的反馈速度。
	* 通过setOnClickListener()方法，Button持有OnClickListener的引用，当用户点击时，Button会调用OnClickListener中的onClick方法，抽象出来就是Button->别观察者、OnClickListener -> 观察者、setOnClickListener -> 订阅，onClicn() -> 事件。

	
	
### 8、RxJava与观察者模式 

	