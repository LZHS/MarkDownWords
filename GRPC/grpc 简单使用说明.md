# grpc 简单使用说明
------------------------------
 
see http://doc.oschina.net/grpc?t=58009
http://blog.csdn.net/kansuke_zola/article/details/53187365?locationNum=4&fps=1


protocol Buffers语法见：[译]Protobuf 语法指南
http://www.colobu.com/2015/01/07/Protobuf-language-guide/


option java_package = "io.grpc.examples";
这个指定的包是为我们生成 Java 类使用的。
option java_multiple_files
指定是否生成多个java文件



要定义一个服务，你必须在你的 .proto 文件中指定 service
共四种类型的service

* 一个 简单 RPC ， 客户端使用存根发送请求到服务器并等待响应返回，就像平常的函数调用一样。
   rpc GetFeature(Point) returns (Feature) {}

* 一个 服务器端流式 RPC ， 客户端发送请求到服务器，拿到一个流去读取返回的消息序列。 客户端读取返回的流，直到里面没有任何消息
  rpc ListFeatures(Rectangle) returns (stream Feature) {}

* 一个 客户端流式 RPC ， 客户端写入一个消息序列并将其发送到服务器，同样也是使用流。一旦 客户端完成写入消息，它等待服务器完成读取返回它的响应。通过在 请求 类型前指定 stream 关键字来指定一个客户端的流方法。
  rpc RecordRoute(stream Point) returns (RouteSummary) {}

* 一个 双向流式 RPC 是双方使用读写流去发送一个消息序列。
  rpc RouteChat(stream RouteNote) returns (stream RouteNote) {}


 生产grpc文件使用说明：
 
 1. 在grpcgenerator下面执行gradle copyTask
  会在tech_module_net_grpc_meta下面产生文件
 2. 如果上个步骤报错，去掉dependsOn build，先手动make一下，然后执行gradlew copyTask
