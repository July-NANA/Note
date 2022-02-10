# Caffeine缓存

参考文档： [Caffeine缓存](https://blog.csdn.net/xiaolyuh123/article/details/78794012)，[Caffeine Cache 进程缓存之王](https://www.jianshu.com/p/15d0a9ce37dd)


新建一个Caffenie缓存对象

```java
Cache<Long, String> IpToCity = Caffeine.newBuilder().build();
```

## Caffeine填充策略

- 手动加载
- 同步加载
- 异步加载

## Caffeine驱逐策略

- 基于大小	
- 基于时间
- 基于引用

