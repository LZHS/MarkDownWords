## 阿里云Centos7下安装Redis及设置外网访问

安装Redis  

* $ wget http://download.redis.io/releases/redis-5.0.2.tar.gz   
* $ tar xzf redis-5.0.2.tar.gz   
* $ cd redis-5.0.2 
* $ make 
* $ make install //将可执行程序复制到/usr/local/bin中 
* $ make test //检查Redis是否编译正确 

> 在执行make test中可能会报以下错误


> * $ You need tcl 8.5 or newer in order to run the Redis test 
make: *** [test] Error 1 

> * 解决办法:


> * $ wget http://downloads.sourceforge.net/tcl/tcl8.6.9-src.tar.gz 
> * $ sudo tar xzvf tcl8.6.9-src.tar.gz -C /usr/local/ 
> * $ cd /usr/local/tcl8.6.9/unix/ 
> * $ sudo ./configure 
> * $ sudo make 
> * $ sudo make install 


**启动Redis**   
1. 直接启动   

> * $ cd redis-4.0.2 
> * $ cd src 
> * $ redis-server  

**目录名-说明**
> * /etc/redis	存放Redis的配置文件
> * /var/redis/端口号	存放Redis的持久化文件

2. 通过初始化脚本启动Redis
(1)配置初始化脚本,将源代码目录里util文件中的redis_init_script文件复制到/etc/init.d目录中,文件名为redis_6379
(2)建立需要的文件夹:
目录名	说明
/etc/redis	存放Redis的配置文件
/var/redis/端口号	存放Redis的持久化文件
(3)修改配置文件,将redis.conf复制到/etc/redis中,以端口号(6379.conf)命名,并对其中部分参数进行编辑: 
参数	值
daemonize	yes
pidfile	/var/run/redis_6379.pid
port	6379
dir	/var/redis/6379
(4)设置redis开机自启


$ cd /etc/init.d 
$ vi redis_6379 //在第二行添加# chkconfig: 2345 10 90 
$ chmod a+x redis_6379 
$ chkconfig --add redis_6379 
$ chkconfig redis_6379 on 

3. 现在可以直接在root下使用redis-cli使用Redis


设置Redis外网访问 
1. 修改配置文件


$ cd redis-4.0.2 
$ vi redis.conf 
//找到bind 127.0.0.1将其编辑为bind 0.0.0.0 



## [mac安装Redis可视化工具-Redis Desktop Manager](https://blog.csdn.net/gavinguo1987/article/details/75125775)

**安装方法**

* 安装brew cask : 在终端中输入下面语句 回车

``` 
ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)" < /dev/null 2> /dev/null ; brew install caskroom/cask/brew-cask 2> /dev/null
```

可能会需要你的mac密码，输入即可

* 安装Redis Desktop Manager
安装完cask之后，在终端中输入 回车