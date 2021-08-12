# CS-PushPlus
 **使用免费且支持微信模板消息推送的 PushPlus 进行上线主机提醒**

> **如果有订阅 ServerChan 的企业微信推送通道可以移步：https://github.com/lintstar/CS-ServerChan**

# 前言

**Mac 版微信目前不支持企业微信消息推送 而 Server 酱从8月开始不再使用微信模板消息通知**

**因此需要换一种新的推送方式**

# 配置相关信息

登录 [PushPlus（推送加）](http://www.pushplus.plus/)

![image-20210812105852128](https://qiniuyun.lintstar.top/hexo/20210812105859.png)

**脚本有两个地方需要替换：**

## PushPlus.py

**http://www.pushplus.plus/push1.html  复制自己的 token 替换到下面的地方**

![image-20210812104818949](https://qiniuyun.lintstar.top/hexo/20210812105905.png)

这里的通知模板支持 Markdown 格式可以随意替换

![image-20210812104840045](https://qiniuyun.lintstar.top/hexo/20210812105908.png)

## PushPuls.cna

**在客户端或者服务端后台挂载时，需要改成 `PushPlus.py` Python 脚本所在的绝对路径（从盘符开始）**

![image-20210812110028880](https://qiniuyun.lintstar.top/hexo/20210812110030.png)

**通过 CobaltStike 服务端 / 客户端 挂载脚本，将上线主机信息通过 PushPlus 微信模板消息通知到微信**

# 服务端后台挂载

**把 cna 脚本添加到本地客户端后，如果beacon上线了，这个提醒的请求是从客户端发出的。**

**如果网络有波动，断开了到 teamserver 的连接，就收不到通知了。**

**解决方法是使用 agscript 在服务器端运行cna文件，和挂载 CobaltStrike 一样，把 cna 脚本也挂载到后台：**

```
 [root@Catherine CS4.3]# screen
 [root@Catherine CS4.3]# ./agscript xx.xxx.xx.xxx [port] Catherine [passwd] CS-PushPlus/PushPlus.cna
 Initial Beacon Checkin: 2122252342 PID: 3488
 Sending server: python3 /root/Tools/CS4.3/CS-PushPlus/PushPlus.py --computernam LINTSTAR82CF --internalip 10.xx.xx.15 --username lintstar
```

**挂载后查看进程：**

```
 [root@Catherine ~]# ps -a
     PID TTY          TIME CMD
 1045504 pts/0    00:00:00 teamserver
 1045507 pts/0    00:00:12 java
 1049085 pts/4    00:00:00 bash
 1049086 pts/4    00:00:08 java
 1055932 pts/7    00:00:00 ps
```

## Agscript 用法

**这里 agscript 的用法为：**

```
 ./agscript [host] [port] [user] [pass] </path/to/file.cna>
```

- **[host] # 服务器的 ip 地址。**
- **[port] # cs 的端口号，启动 cs 时有显示。**
- **[user] # 后台挂载脚本时连接到 teamserver 的用户名。**
- **[pass] # 启动服务端 cs 时设置的密码。**
- **[path] # cna 文件的路径。**

# 效果

## Mac版微信

![image-20210812110851409](https://qiniuyun.lintstar.top/hexo/20210812110851.png)

## 手机微信

![image-20210812111423987](https://qiniuyun.lintstar.top/hexo/20210812111424.png)
