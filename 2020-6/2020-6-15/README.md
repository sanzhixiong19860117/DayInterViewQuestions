# Redis怎么实现分布式锁？

1. SETNX+EXPIRE。非原子性。
2. SET key value [EX seconds] [PX milliseconds] [NX|XX]
   EX second :设置键的过期时间为second秒
   PX millisecond :设置键的过期时间为millisecond毫秒
   NX :只在键不存在时,才对键进行设置操作
   XX:只在键已经存在时,才对键进行设置操作
   SET操作成功完成时,返回OK ,否则返回nil
3. redisson