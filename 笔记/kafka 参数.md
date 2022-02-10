# kafka 参数

```
retries：重试次数，retries = Integer.MAX_VALUE会一直重试直到broker返回ack
retry.backoff.ms：两次重试之间的时间间隔，默认为100，单位是毫秒
```

