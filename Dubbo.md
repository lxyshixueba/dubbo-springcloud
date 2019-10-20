# dubbo-springcloud
dubbo和springcloud面试题

为什么使用dubbo？
使用dubbo可以将核心的业务抽取出来，作为独立的服务，逐渐形成稳定的服务中心，可用于提高业务复用和灵活拓展
分布式架构可以承受更大规模的并发流量

Dubbo和springcloud区别
注册中心不同
服务监控不同
Dubbo没有断路器，都有负载均衡都有服务的路由和过滤
springcloud支持集群选主

dubbo支持的协议
http，redis，hessian（一种序列化的方式，比java的序列化要快）

dubbo内置哪几种容器：
spring，jetty，log4j
Dubbo的容器只是一个简单的main方法，并加载一个spring容器，用于暴露服务

dubbo中的角色节点：
Provider
Consumer
Registry注册中心
monitor 监控之心
container 服务运行容器

服务提供端可以配置的消费端的属性有哪些
1.timeout：方法超时时间
2.retries：失败重试次数
loadbalance：负载均衡算法
actives：最大并发调用限制

Dubbo默认的通信框架：
Netty框架

Dubbo启动时如果依赖的服务不可用：
  假如不可用那么启动时会抛出异常。阻止spring初始化完成。 可以check=false关闭检查
  
Dubbo的序列化架构：  Hessian序列化，Dubbo，FastJson，Java自带序列化

Dubbo的负载均衡算法：
   随机算法：按照配置的权重访问时按照权重随机分配给各个服务节点
   Hash一致性算法：  相同参数的请求发送到同一个消费者
   轮训：按照配置好的权重设置轮询比例
   最少活跃调用数
   
 Dubbo的集群仍错方案： 加起来6种
    失败自动切换。自动重试其他服务器
    失败安全，出现异常时，直接忽略
    快速失败，立即报错，直发器一次调用
  
Dubbo支持服务多协议。
    允许配置多协议。在不同服务上支持不同的协议或者统一服务支持多种协议
  
一个服务接口有多种实现：
    可以用group来分组，服务提供方和消费方指定同一个group
    
服务上线怎么兼容旧版本：
  可以使用版本号区别。不用的版本号注册到注册中心，不同版本相互不引用
  
Dubbo支持声明式缓存，加快热点数据的访问速度

Dubbo服务之间的调用是阻塞的吗？
Tcp：优点
  传输的可靠性高，稳定性强
  高效。字节流传输方式，效率高
  有效性，应用广泛，支持任何平台
  
Nio：一个线程处理多路连接，多路复用。Nio比Tcp需要更少的线程取运行。
Dubbo底层是Nion的非阻塞实现并行调用。客户端不用多个线程就可以实现并行多个远程服务

DUBBO2.0以上支持支持服务降级

DUBBO使用 kill PID来优雅的停机

服务提供者失效提出什么原理？   基于zookeeper的临时节点原理

服务读写推荐的容错侧虐是怎么样的？  
    读操作建议 失败自动切换FailOver  默认重试两次其他服务器
    写操作建议  Failfast快速失败  付一次调用失败就报错

DUBBO必须依赖JDK

Dubbo的管理控制台能做什么？  
管理控制台主要包含：路由规则，动态配置，服务降级，访问控制，权重调整，负载均衡，等管理功能。
  
dubbo服务提供者暴露服务的主过程：
首先 ServiceConfig 类拿到对外提供服务的实际类 ref(如：HelloWorldImpl),然后通过 ProxyFactory 类的 getInvoker 方法使用 ref 生成一个 AbstractProxyInvoker 实例，到这一步就完成具体服务到 Invoker 的转化。
接下来就是 Invoker 转换到 Exporter 的过程
Dubbo 处理服务暴露的关键就在 Invoker 转换到 Exporter 的过程

服务发布过程的一些动作
暴露本地服务
暴露远程服务
启动netty
连接zookeeper
到zookeeper注册
监听zookeeper
一句话概括服务暴露：

Service->Invoker->Exporter

  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
