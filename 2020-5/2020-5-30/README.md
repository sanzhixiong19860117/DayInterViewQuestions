# redis怎么保证高可用，高可用模式有那些?对比下优缺点?

Redis 高可用架构如下：
1.Redis Sentinel 集群 + 内网 DNS + 自定义脚本。
2.Redis Sentinel 集群 + VIP + 自定义脚本。
3.封装客户端直连 Redis Sentinel 端口。
4.JedisSentinelPool，适合 Java。
5.PHP 基于 phpredis 自行封装。
6.Redis Sentinel 集群 + Keepalived/Haproxy。
7.Redis M/S + Keepalived。
8.Redis Cluster。
9.Twemproxy。
10.Codis。


1.Redis Sentinel 集群 + 内网 DNS + 自定义脚本。
优点：
秒级切换；
脚本自定义，架构可控；
对应用透明。
缺点：
维护成本略高；
依赖 DNS，存在解析延时；
Sentinel 模式存在短时间的服务不可用。

2.Redis Sentinel 集群 + VIP + 自定义脚本。
优点：
秒级切换；
脚本自定义，架构可控；
对应用透明。
缺点：
维护成本略高；
Sentinel 模式存在短时间的服务不可用。

3.封装客户端直连 Redis Sentinel 端口。
优点：
服务探测故障及时；
DBA 维护成本低。
缺点：
依赖客户端支持 Sentinel；
Sentinel 服务器需要开放访问权限；
对应用有侵入性。

4.JedisSentinelPool，适合 Java。

5.PHP 基于 phpredis 自行封装。

6.Redis Sentinel 集群 + Keepalived/Haproxy。
优点：
秒级切换；
对应用透明。
缺点：
维护成本高；
存在脑裂；
Sentinel 模式存在短时间的服务不可用。

7.Redis M/S + Keepalived。
优点：
秒级切换；
对应用透明；
部署简单，维护成本低。
缺点：
需要脚本实现切换功能；
存在脑裂。

8.Redis Cluster。
优点：
组件 all-in-box，部署简单，节约机器资源；
性能比 proxy 模式好；
自动故障转移、Slot 迁移中数据可用；
官方原生集群方案，更新与支持有保障。
缺点：
架构比较新，最佳实践较少；
多键操作支持有限（驱动可以曲线救国）；
为了性能提升，客户端需要缓存路由表信息；
节点发现、reshard 操作不够自动化。

9.Twemproxy。
优点：
开发简单，对应用几乎透明；
历史悠久，方案成熟。
缺点：
代理影响性能；
LVS 和 Twemproxy 会有节点性能瓶颈；
Redis 扩容非常麻烦；
Twitter 内部已放弃使用该方案，新使用的架构未开源。

10.Codis。
优点：
开发简单，对应用几乎透明；
性能比 Twemproxy 好；
有图形化界面，扩容容易，运维方便。
缺点：
代理依旧影响性能；
组件过多，需要很多机器资源；
修改了 Redis 代码，导致和官方无法同步，新特性跟进缓慢；
开发团队准备主推基于 Redis 改造的 reborndb。