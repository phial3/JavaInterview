## Redis

* [1.什么是Redis？简述它的优缺点？](#1什么是redis简述它的优缺点)
* [2.Redis相比memcached有哪些优势？](#2redis相比memcached有哪些优势)
* [3.Redis有哪些数据结构？](#3redis有哪些数据结构)
* [4.Redis主要消耗什么物理资源？](#4redis主要消耗什么物理资源)
* [5.Redis的全称是什么？](#5redis的全称是什么)
* [6.一个字符串类型的值能存储最大容量是多少？](#6一个字符串类型的值能存储最大容量是多少)
* [7.Redis为什么那么快？](#7redis为什么那么快)
* [8.Redis如何实现分布式锁？](#8redis如何实现分布式锁)
* [9.Redis是单线程还是多线程？](#9redis是单线程还是多线程)
* [10.Redis 官方为什么不提供 Windows 版本？](#10redis-官方为什么不提供-windows-版本)
* [11.为什么 Redis 需要把所有数据放到内存中？](#11为什么-redis-需要把所有数据放到内存中)
* [12.Redis如何设置密码及验证密码？](#12redis如何设置密码及验证密码)
* [13.Redis集群如何选择数据库？](#13redis集群如何选择数据库)
* [14.缓存失效？缓存穿透？缓存雪崩？缓存并发？](#14缓存失效缓存穿透缓存雪崩缓存并发)
* [15.Redis中的热key怎么处理？](#15redis中的热key怎么处理)
* [16.Redis中的大key怎么处理？](#16redis中的大key怎么处理)
* [17.使用Redis统计网站的UV，应该怎么做？](#17使用redis统计网站的uv应该怎么做)
* [18.Redis事务机制了解过吗？](#18redis事务机制了解过吗)
* [19.Redis key的淘汰策略有哪些？](#19redis-key的淘汰策略有哪些)
* [20.Redis在什么情况下会触发key的回收？](#20redis在什么情况下会触发key的回收)
* [21.Redis的持久化了解过吗？](#21redis的持久化了解过吗)
* [22.Redis在集群种查找key的时候，是怎么定位到具体节点的？](#22redis在集群种查找key的时候是怎么定位到具体节点的)
* [23.Redis集群各个节点之间是怎么保持数据一致性的？](#23redis集群各个节点之间是怎么保持数据一致性的)
* [24.用Redis做延时队列，具体应该怎么实现？](#24用redis做延时队列具体应该怎么实现)
* [25.Redis String的内部编码有哪些？](#25redis-string的内部编码有哪些)
* [26.Redis 集群方案应该怎么做？都有哪些方案？](#26redis-集群方案应该怎么做都有哪些方案)
* [27.Redis 集群方案什么情况下会导致整个集群不可用？](#27redis-集群方案什么情况下会导致整个集群不可用)
* [28.MySQL 里有 2000w 数据，redis 中只存 20w 的数据，如何保证 redis 中的数据都是热点数据？](#28mysql-里有-2000w-数据redis-中只存-20w-的数据如何保证-redis-中的数据都是热点数据)
* [29.Redis有哪些适合的场景？](#29redis有哪些适合的场景)
* [30.Redis和Redisson有什么关系？](#30redis和redisson有什么关系)
* [31.Redis中的管道有什么用？](#31redis中的管道有什么用)
* [32.Redis如何做内存优化？](#32redis如何做内存优化)
* [参考链接](#参考链接)


#### 1.什么是Redis？简述它的优缺点？

Redis本质上是一个Key-Value类型的内存数据库，很像memcached，整个数据库统统加载在内存当中进行操作，定期通过异步操作把数据库数据flush到硬盘上进行保存。

因为是纯内存操作，Redis的性能非常出色，每秒可以处理超过 10万次读写操作，是已知性能最快的Key-Value DB。

Redis的出色之处不仅仅是性能，Redis最大的魅力是支持保存多种数据结构，此外单个value的最大限制是1GB，不像 memcached只能保存1MB的数据，因此Redis可以用来实现很多有用的功能。

比方说用他的List来做FIFO双向链表，实现一个轻量级的高性 能消息队列服务，用他的Set可以做高性能的tag系统等等。

另外Redis也可以对存入的Key-Value设置expire时间，因此也可以被当作一 个功能加强版的memcached来用。 Redis的主要缺点是数据库容量受到物理内存的限制，不能用作海量数据的高性能读写，因此Redis适合的场景主要局限在较小数据量的高性能操作和运算上。

#### 2.Redis相比memcached有哪些优势？

(1) memcached所有的值均是简单的字符串，redis作为其替代者，支持更为丰富的数据类型

(2) redis的速度比memcached快很多

(3) redis可以持久化其数据

#### 3.Redis有哪些数据结构？

Redis 有 5 种基础数据结构，它们分别是：string(字符串)、list(列表)、hash(字典)、set(集合) 和 zset(有序集合)。这 5 种是 Redis 相关知识中最基础、最重要的部分。

#### 4.Redis主要消耗什么物理资源？

内存。

#### 5.Redis的全称是什么？

Remote Dictionary Server。

#### 6.一个字符串类型的值能存储最大容量是多少？

512M

#### 7.Redis为什么那么快？

1、内存操作；
2、单线程，省去线程切换、锁竞争的开销；
3、非阻塞IO模型，epoll。

#### 8.Redis如何实现分布式锁？

详见：https://www.cnblogs.com/wlwl/p/11651409.html

#### 9.Redis是单线程还是多线程？

Redis6.0采用多线程IO，不过命令的执行还是单线程的。
Redis6.0之前，IO线程和执行线程都是单线程的。

#### 10.Redis 官方为什么不提供 Windows 版本？

因为目前 Linux 版本已经相当稳定，而且用户量很大，无需开发 windows 版本，反而会带来兼容性等问题。

#### 11.为什么 Redis 需要把所有数据放到内存中？

Redis 为了达到最快的读写速度将数据都读到内存中，并通过异步的方式将数据写入磁盘。

所以 redis 具有快速和数据持久化的特征，如果不将数据放在内存中，磁盘 I/O 速度为严重影响 redis 的性能。

在内存越来越便宜的今天，redis 将会越来越受欢迎， 如果设置了最大使用的内存，则数据已有记录数达到内存限值后不能继续插入新值。

#### 12.Redis如何设置密码及验证密码？

设置密码：config set requirepass 123456

授权密码：auth 123456

#### 13.Redis集群如何选择数据库？

Redis集群目前无法做数据库选择，默认在0数据库。

#### 14.缓存失效？缓存穿透？缓存雪崩？缓存并发？

1. 缓存失效
   缓存失效指的是大量的缓存在同一时间失效，到时DB的瞬间压力飙升。造成这种现象的原因是，key的过期时间都设置成一样了。解决方案是，key的过期时间引入随机因素，比如5分钟+随机秒这种方式。

2. 缓存穿透
   缓存穿透是指查询一条数据库和缓存都没有的一条数据，就会一直查询数据库，对数据库的访问压力就会增大，缓存穿透的解决方案，有以下2种：
   缓存空对象：代码维护较简单，但是效果不好。
   布隆过滤器：代码维护复杂，效果很好。

3. 缓存雪崩
   缓存雪崩 是指在某一个时间段，缓存集中过期失效。此刻无数的请求直接绕开缓存，直接请求数据库。
   造成缓存雪崩的原因，有以下2种：
   reids宕机。
   大部分数据失效。

对于缓存雪崩的解决方案有以下2种：
搭建高可用的集群，防止单机的redis宕机。
设置不同的过期时间，防止同意之间内大量的key失效。

4. 缓存并发
   有时候如果网站并发访问高，一个缓存如果失效，可能出现多个进程同时查询DB，同时设置缓存的情况，如果并发确实很大，这也可能造成DB压力过大，还有缓存频繁更新的问题。
   一般处理方案是在查DB的时候进行加锁，如果KEY不存在，就加锁，然后查DB入缓存，然后解锁；其他进程如果发现有锁就等待，然后等解锁后再查缓存或者进入DB查询。

#### 15.Redis中的热key怎么处理？

1、对热key进行分散处理。比如：在key上加上不同的前后缀，缓存多个key，使得各个key分散到不同的节点上。
2、采用多级缓存。

#### 16.Redis中的大key怎么处理？

大key指的是value特别大的key。比如很长的字符串，或者很大的set等等。
大key会造成2个问题：1、数据倾斜，比如某些节点内存占用过高。2、当删除大key或者大key自动过期的时候，会造成QPS突降，因为Redis是单线程的缘故。
处理方案：可以将一个大key进行分片处理，比如：将一个大set分成多个小的set。

#### 17.使用Redis统计网站的UV，应该怎么做？

UV与PV不同，UV需要去重。一般有2种方案：
1、用BitMap。存的是用户的uid，计算UV的时候，做下bitcount就行了。
2、用布隆过滤器。将每次访问的用户uid都放到布隆过滤器中。优点是省内存，缺点是无法得到精确的UV。但是对于不需要精确知道具体UV，只需要大概的数量级的场景，是个不错的选择。

#### 18.Redis事务机制了解过吗？

Redis事务的概念：
Redis 事务的本质是一组命令的集合。事务支持一次执行多个命令，一个事务中所有命令都会被序列化。在事务执行过程，会按照顺序串行化执行队列中的命令，其他客户端提交的命令请求不会插入到事务执行命令序列中。
Redis事务就是一次性、顺序性、排他性的执行一个队列中的一系列命令。　　

Redis事务没有隔离级别的概念：
批量操作在发送 EXEC 命令前被放入队列缓存，并不会被实际执行，也就不存在事务内的查询要看到事务里的更新，事务外查询不能看到。
Redis不保证原子性：
Redis中，单条命令是原子性执行的，但事务不保证原子性，且没有回滚。事务中任意命令执行失败，其余的命令仍会被执行。

Redis事务的三个阶段：
开始事务
命令入队
执行事务

Redis事务相关命令：
watch key1 key2 ... : 监视一或多个key,如果在事务执行之前，被监视的key被其他命令改动，则事务被打断 （ 类似乐观锁 ）
multi : 标记一个事务块的开始（ queued ）
exec : 执行所有事务块的命令 （ 一旦执行exec后，之前加的监控锁都会被取消掉 ）　
discard : 取消事务，放弃事务块中的所有命令
unwatch : 取消watch对所有key的监控

#### 19.Redis key的淘汰策略有哪些？

8种：noeviction，volatile-lru，volatile-lfu，volatile-ttl，volatile-random，allkey-lru，allkeys-lfu，allkeys-random

#### 20.Redis在什么情况下会触发key的回收？

2种情况：1、定时（抽样）清理；2、执行命令时，判断内存是否超过maxmemory。

#### 21.Redis的持久化了解过吗？

Redis持久化有RDB和AOF这2种方式。
RDB：将数据库快照以二进制的方式保存到磁盘中。
AOF：以协议文本方式，将所有对数据库进行过写入的命令和参数记录到AOF文件，从而记录数据库状态。

#### 22.Redis在集群种查找key的时候，是怎么定位到具体节点的？

使用crc16算法对key进行hash
将hash值对16384取模，得到具体的槽位
根据节点和槽位的映射信息（与集群建立连接后，客户端可以取得槽位映射信息），找到具体的节点地址
去具体的节点找key
如果key不在这个节点上，则redis集群会返回moved指令，加上新的节点地址给客户端，同时，客户端会刷新本地的节点槽位映射关系
如果槽位正在迁移中，那么redis集群会返回asking指令给客户端，这是临时纠正，客户端不会刷新本地的节点槽位映射关系

#### 23.Redis集群各个节点之间是怎么保持数据一致性的？

主要考察点是Redis的Gossip协议。
详见：https://mp.weixin.qq.com/s/dW0I29Sw86lU0qHpxyhdmw

#### 24.用Redis做延时队列，具体应该怎么实现？

可以使用Zset实现。member是任务描述，score是执行时间，然后用定时器定时去扫描，一旦有执行时间小于或等于当前时间的任务，就立即执行。

#### 25.Redis String的内部编码有哪些？

int、embstr、raw
10000以下的整数会使用缓存里的int常量。
长度小于等于44字节：embstr编码
长度大于44字节：raw编码

#### 26.Redis 集群方案应该怎么做？都有哪些方案？

- codis
- 目前用的最多的集群方案，基本和 twemproxy 一致的效果，但它支持在节点数量改变情况下，旧节点数据可恢复到新 hash 节点。
- redis cluster3.0 自带的集群，特点在于他的分布式算法不是一致性 hash，而是 hash 槽的概念，以及自身支持节点设置从节点。具体看官方文档介绍。
- 在业务代码层实现，起几个毫无关联的 redis 实例，在代码层，对 key 进行 hash 计算，然后去对应的redis 实例操作数据。这种方式对 hash 层代码要求比较高，考虑部分包括，节点失效后的替代算法方案，数据震荡后的自动脚本恢复，实例的监控，等等。
- Java 架构学习资料（里面有高可用、高并发、高性能及分布式、Jvm 性能调优、Spring 源码，MyBatis，Netty,Redis,Kafka,Mysql,Zookeeper,Tomcat,Docker,Dubbo,Nginx 等多个知识点的架构资料）合理利用自己每一分每一秒的时间来学习提升自己，不要再用"没有时间“来掩饰自己思想上的懒惰！趁年轻，使劲拼，给未来的自己一个交代！

#### 27.Redis 集群方案什么情况下会导致整个集群不可用？

有 A，B，C 三个节点的集群,在没有复制模型的情况下,如果节点 B 失败了，那么整个集群就会以为缺少5501-11000 这个范围的槽而不可用。

#### 28.MySQL 里有 2000w 数据，redis 中只存 20w 的数据，如何保证 redis 中的数据都是热点数据？

redis 内存数据集大小上升到一定大小的时候，就会施行数据淘汰策略。

其实面试除了考察 Redis，不少公司都很重视高并发高可用的技术，特别是一线互联网公司，分布式、

JVM、spring 源码分析、微服务等知识点已是面试的必考题。

#### 29.Redis有哪些适合的场景？

（1）会话缓存（Session Cache）

最常用的一种使用Redis的情景是会话缓存（session cache）。用Redis缓存会话比其他存储（如Memcached）的优势在于：Redis提供持久化。当维护一个不是严格要求一致性的缓存时，如果用户的购物车信息全部丢失，大部分人都会不高兴的，现在，他们还会这样吗？

幸运的是，随着 Redis 这些年的改进，很容易找到怎么恰当的使用Redis来缓存会话的文档。甚至广为人知的商业平台Magento也提供Redis的插件。

（2）全页缓存（FPC）

除基本的会话token之外，Redis还提供很简便的FPC平台。回到一致性问题，即使重启了Redis实例，因为有磁盘的持久化，用户也不会看到页面加载速度的下降，这是一个极大改进，类似PHP本地FPC。

再次以Magento为例，Magento提供一个插件来使用Redis作为全页缓存后端。

此外，对WordPress的用户来说，Pantheon有一个非常好的插件 wp-redis，这个插件能帮助你以最快速度加载你曾浏览过的页面。

（3）队列

Reids在内存存储引擎领域的一大优点是提供 list 和 set 操作，这使得Redis能作为一个很好的消息队列平台来使用。Redis作为队列使用的操作，就类似于本地程序语言（如Python）对 list 的 push/pop 操作。

如果你快速的在Google中搜索“Redis queues”，你马上就能找到大量的开源项目，这些项目的目的就是利用Redis创建非常好的后端工具，以满足各种队列需求。例如，Celery有一个后台就是使用Redis作为broker，你可以从这里去查看。

（4）排行榜/计数器

Redis在内存中对数字进行递增或递减的操作实现的非常好。集合（Set）和有序集合（Sorted Set）也使得我们在执行这些操作的时候变的非常简单，Redis只是正好提供了这两种数据结构。

所以，我们要从排序集合中获取到排名最靠前的10个用户–我们称之为“user_scores”，我们只需要像下面一样执行即可：

当然，这是假定你是根据你用户的分数做递增的排序。如果你想返回用户及用户的分数，你需要这样执行：

ZRANGE user_scores 0 10 WITHSCORES

Agora Games就是一个很好的例子，用Ruby实现的，它的排行榜就是使用Redis来存储数据的，你可以在这里看到。

（5）发布/订阅

最后（但肯定不是最不重要的）是Redis的发布/订阅功能。发布/订阅的使用场景确实非常多。我已看见人们在社交网络连接中使用，还可作为基于发布/订阅的脚本触发器，甚至用Redis的发布/订阅功能来建立聊天系统！

#### 30.Redis和Redisson有什么关系？

Redisson是一个高级的分布式协调Redis客服端，能帮助用户在分布式环境中轻松实现一些Java的对象 (Bloom filter, BitSet, Set, SetMultimap, ScoredSortedSet, SortedSet, Map, ConcurrentMap, List, ListMultimap, Queue, BlockingQueue, Deque, BlockingDeque, Semaphore, Lock, ReadWriteLock, AtomicLong, CountDownLatch, Publish / Subscribe, HyperLogLog)。

#### 31.Redis中的管道有什么用？

一次请求/响应服务器能实现处理新的请求即使旧的请求还未被响应。这样就可以将多个命令发送到服务器，而不用等待回复，最后在一个步骤中读取该答复。

这就是管道（pipelining），是一种几十年来广泛使用的技术。例如许多POP3协议已经实现支持这个功能，大大加快了从服务器下载新邮件的过程。

#### 32.Redis如何做内存优化？

尽可能使用散列表（hashes），散列表（是说散列表里面存储的数少）使用的内存非常小，所以你应该尽可能的将你的数据模型抽象到一个散列表里面。

比如你的web系统中有一个用户对象，不要为这个用户的名称，姓氏，邮箱，密码设置单独的key,而是应该把这个用户的所有信息存储到一张散列表里面。

#### 参考链接

http://blog.itpub.net/31545684/viewspace-2213990/

https://blog.csdn.net/weixin_34081595/article/details/92420220