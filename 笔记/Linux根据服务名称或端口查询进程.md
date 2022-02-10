# Linux根据服务名称或端口查询进程

参考文档：[Linux根据服务名称或端口查询进程](https://blog.51cto.com/u_15127576/2766570)

通过端口号查询进程号pId
ps -aux | grep 端口号
ps -ef  | grep 端口号
lsof -i:端口号
lsof -i | grep 端口号

------

通过服务器名称查看进程号pid
ps -aux/ef | grep 服务名称

------

根据进程查看此进程所占用的端口等信息
netstat -nap | grep pid
netstat -ntlp | grep pid

lsof -i | grep pid

此命令可以查端口和进程号 通过lsof -i:只能查端端口号

## 结语

一般知道进程名就可以直接通过
ps进行查看
知道端口的话 lsof 和netstat都能直接查询，然后进而直接查询进程下相关端口

netstat无权限控制，lsof有权限控制，只能看到本用户

lsof能看到pid和用户，可以找到哪个进程占用了这个端口

