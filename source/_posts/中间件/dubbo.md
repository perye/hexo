---
title: dubbo
top: false
cover: false
categories: 中间件
tags:
  - dubbo
keywords: dubbo
abbrlink: 37e41c9c
date: 2020-09-25 13:49:36
---

## dubbo简介

Dubbo是阿里巴巴公司开源的一个高性能优秀的服务框架，使得应用可通过高性能的 RPC 实现服务的输出和输入功能，可以和Spring框架无缝集成。

Dubbo是一款高性能、轻量级的开源Java RPC框架，它提供了三大核心能力：面向接口的远程方法调用，智能容错和负载均衡，以及服务自动注册和发现。

### 基本原理

![dubbo节点](https://perye.oss-cn-shenzhen.aliyuncs.com/blog/java/dubbo/dubbo%E8%8A%82%E7%82%B9.jpg)

节点角色说明

|  节点   | 角色说明  |
|  :----:  | :----:  |
| Provider  | 暴露服务的服务提供方 |
| Consumer  | 调用远程服务的服务消费方 |
| Register  | 服务注册与发现的注册中心 |
| Monitor   | 统计服务的调用次数和调用时间的监控中心 |
| Container | 服务运行容器 |

调用关系说明:

0.服务容器负责启动，加载，运行服务提供者。

1.服务提供者在启动时，向注册中心注册自己提供的服务。

2.服务消费者在启动时，向注册中心订阅自己所需的服务。

3.注册中心返回服务提供者地址列表给消费者，如果有变更，注册中心将基于长连接推送变更数据给消费者。

4.服务消费者，从提供者地址列表中，基于软负载均衡算法，选一台提供者进行调用，如果调用失败，再选另一台调用。

5.服务消费者和提供者，在内存中累计调用次数和调用时间，定时每分钟发送一次统计数据到监控中心。


### 架构设计

![dubbo架构图](https://perye.oss-cn-shenzhen.aliyuncs.com/blog/java/dubbo/dubbo%E6%9E%B6%E6%9E%84%E5%9B%BE.png)

Dubbo框架设计一共划分了10个层:
服务接口层（Service）：该层是与实际业务逻辑相关的，根据服务提供方和服务消费方的业务设计对应的接口和实现。
配置层（Config）：对外配置接口，以ServiceConfig和ReferenceConfig为中心。
服务代理层（Proxy）：服务接口透明代理，生成服务的客户端Stub和服务器端Skeleton。
服务注册层（Registry）：封装服务地址的注册与发现，以服务URL为中心。
集群层（Cluster）：封装多个提供者的路由及负载均衡，并桥接注册中心，以Invoker为中心。
监控层（Monitor）：RPC调用次数和调用时间监控。
远程调用层（Protocol）：封将RPC调用，以Invocation和Result为中心，扩展接口为Protocol、Invoker和Exporter。
信息交换层（Exchange）：封装请求响应模式，同步转异步，以Request和Response为中心。
网络传输层（Transport）：抽象mina和netty为统一接口，以Message为中心。

### 核心功能

**Remoting**:网络通信框架，提供对多种NIO框架抽象封装，包括“同步转异步”和“请求-响应”模式的信息交换方式。

**Cluster**:服务框架，提供基于接口方法的透明远程过程调用，包括多协议支持，以及软负载均衡，失败容错，地址路由，动态配置等集群支持。

**Registry**: 服务注册，基于注册中心目录服务，使服务消费方能动态的查找服务提供方，使地址透明，使服务提供方可以平滑增加或减少机器。

### 应用场景

透明化的远程方法调用，就像调用本地方法一样调用远程方法，只需简单配置，没有任何API侵入。软负载均衡及容错机制，可在内网替代F5等硬件负载均衡器，降低成本，减少单点。服务自动注册与发现，不再需要写死服务提供方地址，注册中心基于接口名查询服务提供者的IP地址，并且能够平滑添加或删除服务提供者。

###  集群容错方案

**FailoverCluster(默认集群容错方案)**：失败自动切换，当出现失败，重试其它服务器。通常用于读操作，但重试会带来更长延迟。
**FailfastCluster**：快速失败，只发起一次调用，失败立即报错。通常用于非幂等性的写操作，比如新增记录。
**FailsafeCluster**：失败安全，出现异常时，直接忽略。通常用于写入审计日志等操作。
**FailbackCluster**：失败自动恢复，后台记录失败请求，定时重发。通常用于消息通知操作。
**ForkingCluster**：并行调用多个服务器，只要一个成功即返回。通常用于实时性要求较高的读操作，但需要浪费更多服务资源。可通过forks=”2″来设置最大并行数。
**BroadcastCluster**：广播调用所有提供者，逐个调用，任意一台报错则报错。通常用于通知所有提供者更新缓存或日志等本地资源信

### 技术点

#### Dubbo和SpringCloud的关系？

| | Dubbo  | Spring Cloud|
|  :----:  | :----:  | :----: |
| 服务注册中心  | Zookeeper | Spring Cloud Netflix Eureka |
| 服务调用方式  | RPC | REST API |
| 服务监控  | Dubbo-monitor | Spring Boot Admin |
| 断路器  | 不完善 | Spring Cloud Netflix Hystrix |
| 服务网关  | 无 | Spring Cloud Netflix Zuul |
| 分布式配置  | 无 | Spring Cloud Config |
| 服务跟踪  | 无 | Spring Cloud Sleuth |
| 消息总线  | 无 | Spring Cloud Bus |
| 数据流  | 无 | Spring Cloud Stream |
| 批量任务  | 无 | Spring Cloud Task |

Dubbo是SOA时代的产物，它的关注点主要在于服务的调用，流量分发、流量监控和熔断。而SpringCloud诞生于微服务架构时代，考虑的是微服务治理的方方面面，另外由于依托了Spirng、SpirngBoot的优势之上，两个框架在开始目标就不一致，Dubbo定位服务治理、SpirngCloud是一个生态。

最大的区别：Dubbo底层是使用Netty这样的NIO框架，是基于TCP协议传输的，配合以Hession序列化完成RPC通信。
而SpringCloud是基于Http协议+Rest接口调用远程过程的通信，相对来说，Http请求会有更大的报文，占的带宽也会更多。但是REST相比RPC更为灵活。

#### 服务调用超时问题怎么解决？

消费者调用服务超时会引起服务降级的发生，即从发出调用请求到获取到提供者的响应结果这个时间超出了设定的时限。默认服务调用超时时限为1秒。可以在消费者端与提供者端设置超时时限来解决。

总的来说还是要设计好业务代码来减少调用时长，设置准确RPC调用的超时时间才能更好的解决这个问题。

全局配置实例
```xml
<!-- 延迟到Spring初始化完成后，再暴露服务,服务调用超时设置为6秒,超时不重试-->    
   <dubbo:provider delay="-1" timeout="6000" retries="0"/>  
```

#### Dubbo支持哪些序列化方式？

默认使用Hessian序列化，还有Duddo、FastJson、Java自带序列化。

#### Dubbo使用的是什么通信框架?

默认使用NIO Netty框架

#### Dubbo服务注册与发现的流程？

流程说明：
Provider(提供者)绑定指定端口并启动服务·指供者连接注册中心，并发本机IP、端口、应用信息和提供服务信息发送至注册中心存储
Consumer(消费者），连接注册中心，并发送应用信息、所求服务信息至注册中心·注册中心根据消费者所求服务信息匹配对应的提供者列表发送至Consumer应用缓存。
Consumer在发起远程调用时基于缓存的消费者列表择其一发起调用。
Provider状态变更会实时通知注册中心、在由注册中心实时推送至Consumer

设计的原因：
Consumer与Provider解偶，双方都可以横向增减节点数。
注册中心对本身可做对等集群，可动态增减节点，并且任意一台宕掉后，将自动切换到另一台去中心化，双方不直接依懒注册中心，即使注册中心全部宕机短时间内也不会影响服务的调用服务提供者无状态，任意一台宕掉后，不影响使用

#### Dubbo在安全机制方面是如何解决的？

Dubbo通过Token令牌防止用户绕过注册中心直连，然后在注册中心上管理授权。Dubbo还提供服务黑白名单，来控制服务所允许的调用方。

#### Dubbo支持哪些协议，每种协议的应用场景，优缺点？

**dubbo 协议**：
Dubbo 默认传输协议
连接个数：单连接
连接方式：长连接
协议：TCP
传输方式：NIO 异步传输
适用范围：传入传出参数数据包较小（建议小于 100K），消费者比提供者个数多，单一 消费者无法压满提供者，尽量不要用 dubbo 协议传输大文件或超大字符串。
**rmi**：采用JDK标准的rmi协议实现，传输参数和返回参数对象需要实现Serializable接口，使用java标准序列化机制，使用阻塞式短连接，传输数据包大小混合，消费者和提供者个数差不多，可传文件，传输协议TCP。多个短连接，TCP协议传输，同步传输，适用常规的远程服务调用和rmi互操作。在依赖低版本的Common-Collections包，java序列化存在安全漏洞；
**webservice**：基于WebService的远程调用协议，集成CXF实现，提供和原生WebService的互操作。多个短连接，基于HTTP传输，同步传输，适用系统集成和跨语言调用；
**http**：基于Http表单提交的远程调用协议，使用Spring的HttpInvoke实现。多个短连接，传输协议HTTP，传入参数大小混合，提供者个数多于消费者，需要给应用程序和浏览器JS调用；
**hessian**：集成Hessian服务，基于HTTP通讯，采用Servlet暴露服务，Dubbo内嵌Jetty作为服务器时默认实现，提供与Hession服务互操作。多个短连接，同步HTTP传输，Hessian序列化，传入参数较大，提供者大于消费者，提供者压力较大，可传文件；
**memcache**：基于memcached实现的RPC协议
**redis**：基于redis实现的RPC协议

#### Dubbo的注册中心集群挂掉，发布者和订阅者之间还能通信么？

可以的，启动dubbo时，消费者会从zookeeper拉取注册的生产者的地址接口等数据，缓存在本地。每次调用时，按照本地存储的地址进行调用。

#### Dubbo集群的负载均衡策略

**random**：随机算法，是 Dubbo 默认的负载均衡算法。存在服务堆积问题。
**roundrobin**：轮询算法。按照设定好的权重依次进行调度。
**leastactive**：最少活跃度调度算法。即被调度的次数越少，其优选级就越高，被调度到的机率就越高。
**consistenthash**：一致性 hash 算法。对于相同参数的请求，其会被路由到相同的提供者。

#### 为什么需要服务治理？

服务治理是主要针对分布式服务框架的微服务，处理服务调用之间的关系、服务发布和发现、故障监控与处理，服务的参数配置、服务降级和熔断、服务使用率监控等。
原因：
过多的服务URL配置困难
负载均衡分配节点压力过大的情况下也需要部署集群
服务依赖混乱，启动顺序不清晰
过多服务导致性能指标分析难度较大，需要监控
故障定位与排查难度较大

#### Dubbo框架源码最重要的设计原则是什么？

Dubbo在设计时具有两大设计原则：
 “微内核+插件”的设计模式。内核只负责组装插件（扩展点），Dubbo的功能都是由插件实现的，也就是 Dubbo 的所有功能点都可被用户自定义扩展类所替换。Dubbo的高扩展性、开放性在这里被充分体现。

采用 URL 作为配置信息的统一格式，所有扩展点都通过传递 URL 携带配置信息。简单来说就是，在Dubbo中，所有重要资源都是以URL的形式来描述的。

#### 为什么Dubbo使用URL，而不使用JSON，使用URL的好处是什么？

首先，Dubbo是将URL作为公共契约出现的，即希望所有扩展点都要遵守的约定。既然是约定，那么可以这样约定，也可以那样约定。只要统一就行。所以，在Dubbo创建之初，也许当时若采用了JSON作为这个约定也是未偿不可的。

其次，单从JSON与URL相比而言，都是一种简洁的数据存储格式。但在简洁的同时，URL与Dubbo应用场景的契合度更高些。因为Dubbo中URL的所有应用场景都与通信有关，都会涉及到通信协议、通信主机、端口号、业务接口等信息。其语义性要强于JSON，且对于这些数据就无需再给出相应的key了，会使传输的数据量更小。

#### Dubbo四大组件间的关系

Dubbo的四大组件为：Consuer、Provider、Registry与Monitor。它们间的关系可以描述为如下几个过程：

**start**：Dubbo服务启动，Spring容器首先会创建服务提供者。
**register**：服务提供者创建好后，马上会注册到服务注册中心Registry，这个注册过程称为服务暴露。服务暴露的本质是将服务名称（接口）与服务提供者主机写入到注册中心Registry的服务映射表中。注册中心充当着“DNS域名服务器”的角色。
**subscribe**：服务消费者启动后，首先会向服务注册中心订阅相关服务。
**notify**：消费者可能订阅的服务在注册中心还没有相应的提供者。当相应的提供者在注册中心注册后，注册中心会马上通知订阅该服务的消费者。但消费者在订阅了指定服务后，在没有收到注册中心的通知之前是不会被阻塞的，而是可以继续订阅其它服务。
**invoke**：消费者以同步或异步的方式调用提供者提供的请求。消费者通过远程注册中心获取到提供者列表，然后消费者会基于负载均衡算法选一台提供者处理消费者的请求。
**count**：每个消费者对各个服务的累计调用次数、调用时间；每个提供者被消费者调用的累计次数和时间，消费者与调用者都会定时发送到监控中心，由监控中心记录。这些统计数据可以在Dubbo的可视化界面看到。

#### Dubbo中配置中心与注册中心的关系

Dubbo中的注册中心是用于完成服务发现的，而配置中心是用于完成配置信息的统一管理的。若没有专门设置配置中心，系统会默认将注册中心服务器作为配置中心服务器。
