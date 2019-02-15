# MAC Flutter 安装总结

Flutter 的安装总体按照[Flutter中文网]里面的步奏来就好，这里只记录我安装Flutter 遇到的问题，首先要学会科学上网，你懂得。


#### 问题一、在跟新IOS插件的时候遇到的问题

```
[✗] iOS toolchain - develop for iOS devices
    ✗ Xcode installation is incomplete; a full installation is necessary for iOS
      development.
      Download at: https://developer.apple.com/xcode/download/
      Or install Xcode via the App Store.
      Once installed, run:
        sudo xcode-select --switch /Applications/Xcode.app/Contents/Developer
    ✗ libimobiledevice and ideviceinstaller are not installed. To install with
      Brew, run:
        brew update
        brew install --HEAD usbmuxd
        brew link usbmuxd
        brew install --HEAD libimobiledevice
        brew install ideviceinstaller
    ✗ ios-deploy not installed. To install with Brew:
        brew install ios-deploy
    ✗ CocoaPods not installed.
        CocoaPods is used to retrieve the iOS platform side's plugin code that
        responds to your plugin usage on the Dart side.
        Without resolving iOS dependencies with CocoaPods, plugins will not work
        on iOS.
        For more info, see https://flutter.io/platform-plugins
      To install:
        brew install cocoapods
        pod setup

```

在此处我遇到了一下问题  

1. ```Error: Your Xcode (9.2) is too outdated.Please update to Xcode 10.1 (or delete it).```  
这个问题很好解决，升级你的XCode就好了，去App Store下载最新的版本。  
2. ```Error: No such keg: /usr/local/Cellar/usbmuxd``` 或者 ```No such file or directory @ dir_chdir - /usr/local/Cellar```或者是```Error: An exception occurred within a child process:
  Errno::EPERM: Operation not permitted @ dir_s_mkdir - /usr/local/Cellar```  
     这个问题我纠结了好久，百度、Google都没有答案，结果发现是该目录不存在，返回到磁盘更目录 返现没有***/usr/local/Cellar***这个目录，直接创建一个目录就好了，再次运行上面的没有问题。

#### 问题二、在使用android studio的时候遇到的问题
步奏如下：  

1. 创建Flutter 项目
2. 注意事项
 
 这里千万不能选择






[Flutter中文网]:https://flutterchina.club/setup-macos/