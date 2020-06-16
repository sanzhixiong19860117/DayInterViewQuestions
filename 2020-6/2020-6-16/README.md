# Redis分布式锁怎么解锁？

1. setnx：del
2. set：lua+del
3. redisson：@Override
       public void unlock(String lockKey) {
           RLock lock = redissonClient.getLock(lockKey);
           lock.unlock();
       }