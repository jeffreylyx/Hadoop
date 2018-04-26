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
一、安装好虚拟后在菜单栏选择编辑→ 虚拟网络编辑器，打开虚拟网络编辑器对话框，选择Vmnet8 Net网络连接方式，随意设置子网IP，点击NAT设置页面，查看子网掩码和网关，后面修改静态IP会用到。  
![Image](/images/1.png)  ![Image](/images/2.png)  ![Image](/images/3.png)  
二、检查宿主机VM8 网卡设置，打开网络和共享中心→ 更改适配器设置→，在VMware Network Adapter VMnet8上单击右键，选择属性按钮打开属性对话框。（这个在服务器上修改了，但是没啥用，还是无法上网，但是能满足局域网内其他计算机能连接服务器上的虚拟机就好了）  
![Image](/images/4.png)  ![Image](/images/5.png)  
三、在虚拟机右下角，点击网络适配器按钮，右键选择断开连接，然后再重新连接，确保刚才的设置生效。然后开启虚拟机，输入ifcfg查看当前分配的IP。  
![Image](/images/6.png)  ![Image](/images/7.png)  
四、最重要的环节  
vi /etc/sysconfig/network-scripts/ifcfg-eth0
 ```
  DEVICE="eth0"
  BOOTPROTO="static"
  HWADDR="00:0C:29:5B:67:42"(这个地址每个虚拟机都不同，默认的是正确的，不要修改)
  IPADDR=192.168.1.60
  NETMASK=255.255.255.0
  DNS1=192.168.1.2
  GATEWAY=192.168.1.2
  IPV6INIT="yes"
  NM_CONTROLLED="yes"
  ONBOOT="yes"
  TYPE="Ethernet"
  UUID="cbee3985-9e8a-46dd-b557-506e8ad261d3"
```   
OK，成功设置静态IP。
### 2.配置各台虚拟机之间的ssh
一、修改机器名  
vi /etc/sysconfig/network  
修改hostname  
二、关闭防火墙    
chkconfig iptables off(永久关闭)  
三、修改hosts文件  
vi /etc/hosts  
添加机器名以及IP,类似于 master 192.168.1.60  
windows也需要修改：C:\Windows\System32\drivers\etc\hosts  
四、创建用户组  
我直接用的root，还是root用起来最直接：)  
五、配置SSH  
ssh -keygen -t rsa 后面直接回车  
会生成/root/.ssh目录，将目录里的公钥id_rsa.pub复制为authorized_keys，依次分发到各个从机中  
### 3.安装JDK,HADOOP,ZOOKEEPER和HBASE



