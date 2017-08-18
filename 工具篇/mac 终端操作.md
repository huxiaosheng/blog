# mac 终端操作



## mac端口占用情况

### 使用lsof命令

```
losf命令可以列出当前的所有网络情况
-n 表示主机以ip地址显示
-p 表示端口以数字形式显示，默认为端口名称
-i 意义较多，具体man losf,主要是用来过滤losf的输出结果
-s 和 -i 配合使用，用于过滤输出
```



**查看某端口使用情况**

> lsof -i:3000

控制台输出:

```
huyuandeMacBook-Pro:~ huyuan$ lsof -i tcp:3000
COMMAND     PID   USER   FD   TYPE             DEVICE SIZE/OFF NODE NAME
Google    43885 huyuan  137u  IPv4 0x7f46cdba233aa7b1      0t0  TCP localhost:53125->localhost:hbci (CLOSE_WAIT)
Google    43885 huyuan  149u  IPv4 0x7f46cdba24b630a9      0t0  TCP localhost:53130->localhost:hbci (CLOSE_WAIT)
Google    43885 huyuan  173u  IPv4 0x7f46cdba24eca5c1      0t0  TCP localhost:53131->localhost:hbci (CLOSE_WAIT)
Google    43885 huyuan  200u  IPv4 0x7f46cdba24e515c1      0t0  TCP localhost:53129->localhost:hbci (CLOSE_WAIT)
Google    43885 huyuan  201u  IPv4 0x7f46cdba249a07b1      0t0  TCP localhost:53133->localhost:hbci (CLOSE_WAIT)
Google    43885 huyuan  203u  IPv4 0x7f46cdba275489a1      0t0  TCP localhost:53135->localhost:hbci (CLOSE_WAIT)
Google    43885 huyuan  225u  IPv4 0x7f46cdba24ecaeb9      0t0  TCP localhost:53140->localhost:hbci (ESTABLISHED)
node      55735 huyuan   16u  IPv4 0x7f46cdba248749a1      0t0  TCP *:hbci (LISTEN)
node      55735 huyuan   18u  IPv4 0x7f46cdba24b639a1      0t0  TCP localhost:hbci->localhost:53140 (ESTABLISHED)
```



**杀掉进程，执行：**

> kill -9 55735







