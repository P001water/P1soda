![image-20240829092224067](./img/image-20240829092224067.png)

<h3 align="center">P1soda 一款更高、更快、更强的全方位内网扫描工具</h3>

---



P1soda （苏打水）是一款常规内网渗透场景下的全方位漏洞扫描工具，Powered by P001water





# 功能特色

* 主机存活探测

充分适应内网场景，ip输入，支持ICMP echo发包探测、ping命令探测

* 端口指纹识别

基于nmap-service-probes指纹实现的Mini nmap端口指纹识别引擎，出于工具体积和最小化请求原则只是从全部指纹中提取关键指纹

如下14条nmap Probe，支持指纹识别如下协议服务：

```
ftp
monetdb
mysql
ssh
postgresql
socks5
socks4
JDWP
mssql
memcached
redis
adb
VNC
```

* web 侧信息探测

http请求时User-Agent头随机化，基本web信息探测，http响应状态码，webTitle标题等

* web 重点资产指纹识别

从P1finger中精简的内网常见系统的指纹

* OXID Resolver DCOM接口未授权网卡探测

socket Raw连接发包解决，避免调包，最小化工具体积

* NetBIOS 137 139 主机信息探测

137 NBNS、139 NTLMSSP协议中的主机信息提取，137 NBNS协议域控识别

* 常见服务爆破功能，例如ssh、ftp、mysql、vnc等等

根据返回报文更加智能化的服务爆破，减少无用的爆破，目前支持爆破模块

```
Ftp
mysql
ssh
vnc
```

* web 漏洞检测

从头实现的Mini Nuclei引擎，体积小于 2 M，支持nuclei的POC

* socks5、http代理使用

支持socks5、http代理使用

* MS-17010检测，redis，vnc未授权检测等等



​	

# 基本使用

工具参数如下图，默认情况下不开启服务爆破功能

![image-20240909001216321](./img/image-20240909001216321.png)

* 入门使用

单个、多个目标探测，支持网段输入

```
P1soda.exe -t 192.168.110.235 	// 单个目标
P1soda.exe -t 192.168.110.2-235 // 多个目标
P1soda.exe -t 192.168.110.143,192.168.110.251 // 多个目标
P1soda.exe -t 192.168.110.235/24 // 扫描110 C段
```

![image-20240908233120141](./img/image-20240908233120141.png)

* C 段探测

-tc 指定ip即可，自动探测ip所在C段

```
.\P1soda.exe -tc 192.168.110.229 -br // -br 开启爆破功能

.\P1soda.exe -tc 192.168.110.229,192.168.1.1 // 探测192.168.110.229,192.168.1.1两个C段
```

![image-20240908232605907](./img/image-20240908232605907.png)

* 指定用户名密码爆破

```
.\P1soda.exe -t 127.0.0.1 -br -user root,admin -pwd 123456 // -br 开启爆破模式，默认情况不开启
```

![image-20240908233510469](./img/image-20240908233510469.png)

* 输出保存文件

```
.\P1soda.exe -t 127.0.0.1 -br -nc -o // -br开启爆破模式, -o输出重定向到p1.txt, -nc取消颜色输出
```

![image-20240908233701996](./img/image-20240908233701996.png)

* 针对url的检测

单个url目标

```
.\P1soda.exe -u http://192.168.110.251
```

![image-20240909000500045](./img/image-20240909000500045.png)

多个目标

```
.\P1soda.exe -uf .\targets.txt
```

![image-20240908235659706](./img/image-20240908235659706.png)

* Debug 测试信息

```
.\P1soda.exe -u http://192.168.110.143:8888 -dbg
```

debug显示一些poc信息，http请求信息

![image-20240909005651301](./img/image-20240909005651301.png)

* 网段探测

更多功能，正在设计中，敬请期待......





# 更新日志



v0.0.1

1. 基本功能更新

v0.0.2

1. 增加网段输入方法，比如扫描C段，P1soda -t 192.168.110.1/24
2. 修改http/https判断功能
3. 增加poc和指纹信息

v0.0.3

1. 添加默认扫描端口（fofa上的vnc端口top 5）
2. 增加vnc服务未授权识别和爆破

<img src="./img/image-20241013191315747.png" alt="image-20241013191315747" style="zoom: 33%;" />

v0.0.4

1. redis 未授权检测和系统信息提取

<img src="./img/image-20241022001135114.png" alt="image-20241022001135114" style="zoom:33%;" />

2. ms17010永恒之蓝检测 （没研究过，抄的k8gege的）

<img src="./img/image-20241022001225844.png" alt="image-20241022001225844" style="zoom:33%;" />

3. hikivision版本信息检测和漏洞poc添加

<img src="./img/image-20241022010715099.png" alt="image-20241022010715099" style="zoom:33%;" />

