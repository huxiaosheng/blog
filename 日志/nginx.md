# Nginx

[TOC]

Nginx 是一个十分轻量级的HTTP服务器。同IIS、Apache 、Tomcat都属于Web服务器。不仅响应静态页面的速度非常快，而且它的模块数量达到 Apache 的近 2/3。对 proxy 和 rewrite 模块的支持很彻底，还支持 mod_fcgi、ssl、vhosts ，适合用来做 mongrel clusters 的前端 HTTP 响应。



## 特点

- 处理静态文件，索引文件以及自动索引；打开文件描述符缓冲．
- 无缓存的反向代理加速，简单的负载均衡和容错．
- FastCGI，简单的负载均衡和容错．
- 模块化的结构。包括 gzipping, byte ranges, chunked responses,以及 SSI-filter 等 filter。如果由 FastCGI 或其它代理服务器处理单页中存在的多个 SSI，则这项处理可以并行运行，而不需要相互等待。
- 支持 SSL 和 TLSSNI．



## 配置

Nginx 的配置系统由一个主配置文件和其他一些辅助的配置文件构成。这些配置文件均是纯文本文件，全部位于Nginx 安装目录下的 conf 目录下。

配置文件中以`#`开始的行，或者是前面有若干空格或者 TAB，然后再跟`#`的行，都被认为是注释，也就是只对编辑查看文件的用户有意义，程序在读取这些注释行的时候，其实际的内容是被忽略的。





### 指令上下文

nginx.conf 中的配置信息，根据其逻辑上的意义，对它们进行了分类，也就是分成了多个作用域，或者称之为配置指令上下文。不同的作用域含有一个或者多个配置项。

当前 Nginx 支持的几个指令上下文：

- main: Nginx 在运行时与具体业务功能（比如http服务或者email服务代理）无关的一些参数，比如工作进程数，运行的身份等。
- http: 与提供 http 服务相关的一些配置参数。例如：是否使用 keepalive 啊，是否使用gzip进行压缩等。
- server: http 服务上支持若干虚拟主机。每个虚拟主机一个对应的 server 配置项，配置项里面包含该虚拟主机相关的配置。在提供 mail 服务的代理时，也可以建立若干 server，每个 server 通过监听的地址来区分。
- location: http 服务中，某些特定的URL对应的一系列配置项。
- mail: 实现 email 相关的 SMTP/IMAP/POP3 代理时，共享的一些配置项（因为可能实现多个代理，工作在多个监听地址上）。

