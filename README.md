# Hadoop
Hadoop Distributed File System and Mapreduce
## 环境搭建

|虚拟机系统|机器名称|IP地址|
|---|:---:|---|
|Centos 6.5|master|192.168.1.60|
|Centos 6.5|slave1|192.168.1.61|
|Centos 6.5|slave2|192.168.1.62|
|Centos 6.5|slave3|192.168.1.63|
|Centos 6.5|slave4|192.168.1.64|

### 1.配置每台虚拟机的静态IP
1安装好虚拟后在菜单栏选择编辑→ 虚拟网络编辑器，打开虚拟网络编辑器对话框，选择Vmnet8 Net网络连接方式，随意设置子网IP，点击NAT设置页面，查看子网掩码和网关，后面修改静态IP会用到。
！[Image](/images/1.png)
