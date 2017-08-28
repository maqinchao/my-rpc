# my-rpc  
>了解dubbo的一些原理后，想尝试自己编写rpc，加深了解。

个人对rpc原理的见解
---
>rpc是一种远程过程调用协议。rpc主要功能：异构分布式项目之间的通信，使消费者只需要知道接口，远程调用方法就像调用本地方法一样。
要使得消费层只通过接口调用远程实现方法，那么其之间的传输数据肯定是：类、方法、参数、返回值，以及一些其它传输的信息。
之间涉及到通信，肯定要发布服务供客户端请求。客户端要执行未知实现的方法，是通过动态代理实现的。
在了解动态代理的使用后，就会发现，在动态代理的方法执行过程中，可以不用去执行真实方法（invoke方法中），你可以获取到上面所需要的类、方法、参数、返回值等执行方法的参数。
那么把这些参数传输到远程去。在提供层接收到消费层方法的传参后，通过反射执行已经注册的类方法。（提供层要把暴露接口的实现类的方法注册到容器中，供查找）  

个人认为dubbo的优势
--  
* 拥有丰富的通信方式、多种协议。
* 有完善的负载、集群容错、负载均衡机制。
* 可搭配多种
服务注册中心


自己编写rpc之前的所需的准备
--
>了解了常用rpc框架dubbo的流程。复习了动态代理。复习了java io通信。

模块说明    
------
#### rpc-core
>这个模块是rpc的核心部分包括网络通信，客户端动态代理，通信数据结构  
#### rpc-service  
>这个模块rpc提供层暴露的接口
####  rpc-provider  
>这个模块是rpc的提供层 
####  rpc-consumer
>这个模块是rpc的消费层 

依赖关系
---
>rpc-consumer、rpc-provider为rpc使用方，所以他们两个都依赖 rpc-core 模块。
因为提供层要为消费层暴露接口，所以提取了公共接口，因此，它们两个都依赖rpc-service


启动调试*HelloWorld*
--
>使用HelloService接口进行调试。首先运行zookeeper服务，默认本地ip。接着启动提供层：在rpc-provider模块中运行top.yuyufeng.rpc.ServerApp.Main
然后启动消费层：在rpc-consumer模块中运行top.yuyufeng.rpc.test.ClientApp.Main

更新日志
----
>2017年8月24日 使用*zookeeper*来作协调服务注册与发现,使用*Protostuff*序列化(取代jdk序列化)
之前初始版本已经建立分支[https://github.com/yyfyyf1994/my-rpc/tree/v1](https://github.com/yyfyyf1994/my-rpc/tree/v1)  
>2017年8月28日 将原来的BIO通信改成了NIO，加入Netty4进行通信 
之前初始版本已经建立分支[https://github.com/yyfyyf1994/my-rpc/tree/v2](https://github.com/yyfyyf1994/my-rpc/tree/v2)