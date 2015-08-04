> nginx的详细配置字段分别有什么作用？

##nginx.conf配置文件详解
```
user  www-data;   //运行用户
worker_processes 4;   //启动的进程数量，一般设置成与CPU核数相等
error_log  var/log/nginx/error.log;   //全局错误日志
pid   /var/run/nginx.pid; 全局PID文件
events {}
```
