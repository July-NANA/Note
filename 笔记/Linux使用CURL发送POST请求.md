# Linux使用CURL发送POST请求

参考文档: [使用 curl 发送 POST 请求](https://blog.csdn.net/m0_37886429/article/details/104399554)

## 一、 参数说明

**格式：** `curl -H 请求头 -d 请求体 -X POST 接口地址`



| 参数              | 内容     | 格式                                                         |
| ----------------- | -------- | ------------------------------------------------------------ |
| -H（或者-header） | 请求头   | "Content-Type: application/json"                             |
| -d                | POST内容 | ‘{“id”: “001”, “name”:“张三”, “phone”:“13099999999”}’ 或者<br/>‘id=001&name=张三&phone=13099999999’ |
| -X                | 请求协议 | POST、GET、DELETE、PUSH、PUT、OPTIONS、HEAD                  |

## 二、实例

```
curl -H "Content-Type: application/json" -X POST -d "name='张三'" http://localhost:8080/api
```

