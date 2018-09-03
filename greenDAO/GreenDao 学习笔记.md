# GreenDao 学习笔记


### 一、GreenDao简介
greenDao 是一款面向Android的轻便、快捷的ORM框架，将Java对象映射到SQLite数据库中，我们操作数据库的时候，不需要在编写复杂的SQL语句，在性能方面，greenDao针对Android进行了高度优化，最小的内存开销，依赖体积小，同事还是支持数据库加密。

### 二、GreenDao特征
1、  对象映射  
greenDao是ORM框架，可以非常便捷的将Java对象映射到SQLite数据库中保存。  

2、高性能  
ORM框架有很多，比较著名的有OrmLite,ActiveAndroid等，性能也不一样，但是greenDao性能是优于其他两个框架的。  

3、支持加密  
greenDao 是支持加密的，可以安全的保存用户数据  

4、轻量级  
greenDao核心库小于10K,所以我们并不担心添加greenDao后APK大小是否庞大  

5、支持protocol buffer (protobuf) 协议  
greenDAO支持protocol butffer(protobuf)协议数据直接存储，如果你通过protobuf协议与服务器交互，将不需要任何的映射。  

6、代码生成  
greenDAO会根据配置信息自动生成核心管理类以及DAO对象

7、开源  
greenDAO是开源的，我们可以在GitHub上下载源码学习  
 [github地址](https://github.com/greenrobot/greenDAO)
 

### 核心类介绍  
* DaoMaster:  
	使用greenDao的入口点。DaoMaster负责管理数据库对象（SQLiteDatabase）和DAO类（对象），我们可以通过它内部类OpenHelper和DevOpenHelper SQLLiteOpenHepler创建不同模式的SQLite数据库。  
* DaoSession:  
	管理制定模式下的所有DAO对象，DaoSession提供了一些通用的持久性方法，比如插入、负载、更新、更新和删除实体。  
* XxxDAO:
	每个实体类greenDAO都会生成一个与之对应的DAO对象，如User实体，则会生成一个一个UserDao类。
* Entities:
	可持久话对象，通常实体对象代表了一个数据库使用标准Java属性（如一个POJO 或 JavaBean）。

