## Redis

> 注意!!!
> ：下面这些问题的参考答案你几乎都可以在 [JavaGuide 在线阅读网站](https://javaguide.cn/database/mysql/mysql-questions-01.html)
> 和 《JavaGuide 面试指北》中找到。并且，这两个参考资料没有给出解答的问题，我也都给了对应的参考文章。
>
> 建议你先阅读学习了对应的内容之后再进行自测。

### Redis 基础

#### Redis 有什么作用?为什么要用 Redis/为什么要用缓存？

👉 重要程度：⭐⭐⭐

💡 提示：内存数据库，高并发，常用来做缓存。

#### Redis 除了做缓存，还能做什么？

👉 重要程度：⭐⭐⭐⭐

💡 提示：分布式锁、限流、消息队列（不推荐）。另外，利用 Redis 自带的数据结构我们可以很方便地完成很多复杂的业务场景比如通过
sorted set 维护一份排行榜。

#### Redis 可以做消息队列么？

👉 重要程度：⭐⭐⭐

💡 提示：Redis 5.0 新增加的一个数据结构 Stream 可以用来做消息队列。不过，和专业的消息对象相比还是有很多欠缺的地方。

#### 分布式缓存常见的技术选型方案有哪些？

👉 重要程度：⭐⭐⭐

💡 提示：Memcached 和 Redis。紧接着面试官可能会让你简单对比一下 Memcached 和 Redis 。

### Redis 数据结构

#### Redis 常用的数据结构有哪些？

👉 重要程度：⭐⭐⭐⭐

💡 提示：

- 5 种基础数据类型：String（字符串）、List（列表）、Set（集合）、Hash（散列）、Zset（有序集合）。

- 3 种特殊数据类型：HyperLogLogs（基数统计）、Bitmap （位存储）、geospatial (地理位置)。

面试官问到 Redis 常用的数据结构之后，可以会顺带问你 Redis 底层数据结构。

#### 使用 Redis 统计网站 UV 怎么做？

👉 重要程度：⭐⭐⭐⭐⭐

💡 提示：可以借助 HyperLogLog 来做，占用空间非常非常小。

#### 使用 Redis 实现一个排行榜怎么做？

👉 重要程度：⭐⭐⭐⭐⭐

💡 提示：Redis 中有一个叫做 sorted set 的数据结构经常被用在各种排行榜的场景下。

### Redis 线程模型

#### Redis 单线程模型了解吗？

👉 重要程度：⭐⭐⭐⭐⭐

💡 提示：Redis 通过 IO 多路复用程序 来监听来自客户端的大量连接（或者说是监听多个
socket），它会将感兴趣的事件及类型（读、写）注册到内核中并监听每个事件是否发生。

类似问题：既然是单线程，那怎么监听大量的客户端连接呢？、为什么 Redis 这么快？

#### Redis6.0 之前为什么不使用多线程？

👉 重要程度：⭐⭐⭐

💡 提示：单线程编程容易并且更容易维护、Redis 的性能瓶颈不在 CPU 。

#### Redis6.0 之后为何引入了多线程？

👉 重要程度：⭐⭐⭐⭐

💡 提示：Redis6.0 引入多线程主要是为了提高网络 IO 读写性能。

### Redis 内存管理

#### Redis 给缓存数据设置过期时间有啥用？

👉 重要程度：⭐⭐⭐⭐

💡 提示：内存是有限的，如果缓存中的所有数据都是一直保存的话，分分钟直接 Out of memory。

#### Redis 是如何判断数据是否过期的呢？

👉 重要程度：⭐⭐⭐⭐

💡 提示：Redis 通过一个叫做过期字典（可以看作是 hash 表）来保存数据过期的时间。

#### 过期的数据的删除策略了解么？

👉 重要程度：⭐⭐⭐⭐

💡 提示：定期删除对内存更加友好，惰性删除对 CPU 更加友好。两者各有千秋，所以 Redis 采用的是 定期删除+惰性/懒汉式删除 。

#### Redis 内存淘汰机制了解么？

👉 重要程度：⭐⭐⭐⭐

💡 提示：Redis 提供 6 种数据淘汰策略。

类似问题：MySQL 里有 2000w 数据，Redis 中只存 20w 的数据，如何保证 Redis 中的数据都是热点数据?

### Redis 持久化机制

#### 怎么保证 Redis 挂掉之后再重启数据可以进行恢复？

👉 重要程度：⭐⭐⭐⭐⭐

💡 提示：依赖持久化机制。

#### 什么是 RDB 持久化？

👉 重要程度：⭐⭐⭐⭐⭐

💡 提示：Redis 可以通过创建快照来获得存储在内存里面的数据在某个时间点上的副本。

#### 什么是 AOF 持久化？

👉 重要程度：⭐⭐⭐⭐⭐

💡 提示：开启 AOF 持久化后每执行一条会更改 Redis 中的数据的命令，Redis 就会将该命令写入到内存缓存 server.aof_buf 中，然后再根据
appendfsync 配置来决定何时将其同步到硬盘中的 AOF 文件。

#### Redis 4.0 对于持久化机制做了什么优化？

👉 重要程度：⭐⭐⭐⭐

💡 提示：Redis 4.0 开始支持 RDB 和 AOF 的混合持久化（默认关闭，可以通过配置项 aof-use-rdb-preamble 开启）。

### Redis 事务

#### 如何使用 Redis 事务？

👉 重要程度：⭐⭐⭐⭐

💡 提示：Redis 可以通过 MULTI，EXEC，DISCARD 和 WATCH 等命令来实现事务(transaction)功能。

#### Redis 事务支持原子性吗？

👉 重要程度：⭐⭐⭐⭐

💡 提示：Redis 事务在运行错误的情况下，除了执行过程中出现错误的命令外，其他命令都能正常执行。并且，Redis 是不支持回滚（roll
back）操作的。因此，Redis 事务其实是不满足原子性的（而且不满足持久性）。

#### Redis 事务还有什么缺陷？

👉 重要程度：⭐⭐⭐⭐

💡 提示：除了不满足原子性之外，事务中的每条命令都会与 Redis 服务器进行网络交互，这是比较浪费资源的行为。明明一次批量执行多个命令就可以了，这种操作实在是看不懂。

#### 如何解决 Redis 事务的缺陷？

👉 重要程度：⭐⭐⭐⭐

💡 提示：Lua 脚本、 [Redis functions](https://redis.io/docs/manual/programmability/functions-intro/)。

### Redis 性能优化

#### 什么是 bigkey？有什么危害？

👉 重要程度：⭐⭐⭐

💡 提示：一个 key 对应的 value 所占用的内存比较大。bigkey 会消耗更多的内存空间，也会影响到性能。

#### 如何发现 bigkey？

👉 重要程度：⭐⭐⭐

💡 提示：使用 Redis 自带的 --bigkeys 参数来查找或者分析 RDB 文件。

#### 如何避免大量 key 集中过期？

👉 重要程度：⭐⭐⭐⭐⭐

💡 提示：给 key 设置随机过期时间 + 开启 lazy-free（惰性删除/延迟释放）。

#### 什么是 Redis 内存碎片?为什么会有 Redis 内存碎片?

👉 重要程度：⭐⭐⭐⭐

💡 提示：内存碎片简单地理解为那些不可用的空闲内存。

### Redis 生产问题

#### 什么是缓存穿透？怎么解决？

👉 重要程度：⭐⭐⭐⭐⭐

💡 提示：大量请求的 key 根本不存在于缓存中，导致请求直接到了数据库上。常见的解决办法如下：

- 缓存无效 key

- 布隆过滤器

#### 什么是缓存雪崩？怎么解决？

👉 重要程度：⭐⭐⭐⭐⭐

💡 提示：缓存在同一时间大面积的失效，后面的请求都直接落到了数据库上，造成数据库短时间内承受大量请求。 如果是 Redis
服务不可用的情况的话，我们应该搭建 Redis 集群来避免单点风险。如果是缓存过期的话，参考“如何避免大量 key 集中过期？”这个问题。

#### 如何保证缓存和数据库数据的一致性？

👉 重要程度：⭐⭐⭐⭐⭐

💡 提示：3 种常见的缓存读写策略。

### Redis 集群

#### 如何保证 Redis 服务高可用？

👉 重要程度：⭐⭐⭐⭐⭐

💡 提示：Redis Sentinel 集群。

#### Sentinel（哨兵） 有什么作用？

👉 重要程度：⭐⭐⭐⭐

💡 提示：监控 Redis 节点的运行状态并自动实现故障转移。

#### Redis 缓存的数据量太大怎么办?

👉 重要程度：⭐⭐⭐⭐⭐

💡 提示：Redis Cluster。

#### Redis Cluster 虚拟槽分区有什么优点？

👉 重要程度：⭐⭐⭐⭐

💡 提示：解耦了数据和节点之间的关系，提升了集群的横向扩展性和容错性。

#### Redis Cluster 中的各个节点是如何实现数据一致性的？

👉 重要程度：⭐⭐⭐⭐

💡 提示：Gossip 协议