## 获得Stream 的方法  
- 通过构造函数
- 使用StreamController
- IO Stream

### Stream 有三个构造方法
- **Stream.formFuture：** 从Future创建单订阅流，当Future完成时触发一个data或者error，然后使用Down事件关闭这个流。
* **Stream.formFutures** :从一组Future创建一个单订阅流，每个future都有自己的data或者error事件，当整个Futures完成后，流将会关闭。如果Futures为空，流将会立刻关闭。
* **Stream.fromIterable** :创建从一个集合中获取其数据的单订阅流。

```

Stream.fromInterable([1,2,3]);

```

## 监听Stream的方法
监听一个流最常见的方法就是listen。当有事件发出时，流将会通知listener。Listen方法提供了这几种触发事件：

- **onData(必填)**:收到数据时触发
- **onError** :收到Error时触发
- **onDone** :结束时触发
- **unsubscribeOnError** :

// TODO https://www.jianshu.com/p/a5d7758938ef