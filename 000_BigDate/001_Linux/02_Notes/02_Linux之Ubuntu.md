# Linux之Ubuntu

## 1.安装

### 1.1 过程

+ <img src="02_Linux%E4%B9%8BUbuntu.assets/image-20210112085342341.png" alt="image-20210112085342341" style="zoom: 67%;" />

+ <img src="02_Linux%E4%B9%8BUbuntu.assets/image-20210112085446002.png" alt="image-20210112085446002" style="zoom: 67%;" />
+ <img src="02_Linux%E4%B9%8BUbuntu.assets/image-20210112085555770.png" alt="image-20210112085555770" style="zoom: 67%;" />
+ <img src="02_Linux%E4%B9%8BUbuntu.assets/image-20210112085631689.png" alt="image-20210112085631689" style="zoom: 67%;" />

### 1.2 磁盘分区

+ <img src="02_Linux%E4%B9%8BUbuntu.assets/image-20210112085653961.png" alt="image-20210112085653961" style="zoom: 67%;" />
+ <img src="02_Linux%E4%B9%8BUbuntu.assets/image-20210112085827034.png" alt="image-20210112085827034" style="zoom:67%;" />
+ <img src="02_Linux%E4%B9%8BUbuntu.assets/image-20210112090135360.png" alt="image-20210112090135360" style="zoom:67%;" />
+ <img src="02_Linux%E4%B9%8BUbuntu.assets/image-20210112090244737.png" alt="image-20210112090244737" style="zoom:67%;" />
+ <img src="02_Linux%E4%B9%8BUbuntu.assets/image-20210112090425663.png" alt="image-20210112090425663" style="zoom: 67%;" />
+ VMware安装虚拟机时最好设置50G以上，后续文件和快照较多。
+ <img src="02_Linux%E4%B9%8BUbuntu.assets/image-20210112090547336.png" alt="image-20210112090547336" style="zoom:67%;" />
+ 接下来continue就可以

### 1.3 后续

+ <img src="02_Linux%E4%B9%8BUbuntu.assets/image-20210112090710872.png" alt="image-20210112090710872" style="zoom:67%;" />
+ <img src="02_Linux%E4%B9%8BUbuntu.assets/image-20210112090854257.png" alt="image-20210112090854257" style="zoom:67%;" />
+ 然后等待安装完成吧

## 2.进入后常规

### 2.1 命令思想

在Ubuntu中安装时没有设置root用户，故许多命令需要`sudo`来提升权限。

### 2.2 进入root用户

因为安装时未设置root用户密码，所以

+ 在普通用户下，`sudo passwd root`
+ 设置密码
+ `su root`进入root用户

### 2.3 进入文本编辑模式

15版本以上`systemctl set-default multi-user.target `然后重启

### 2.4 配网(指定静态ip)

先 `ip addr`查看网卡，如果是`ens33`则第一种，是`enp0s3`或`enp0s8`则第二种。

+ 17版本之前的也是第一种
+ 17版本后可能有这两种

#### 2.4.1 ens33

+ 配置ip

  + 进入文件`cd /etc/network/`

  + 编辑 interfaces 文件`vi interfaces`

    + ```bash
      auto ens33   #网卡名
      iface ens33 inet static   #静态
      address 192.168.10.104    #IP地址，根据个人的vmnet8网段或主机网段写
      gateway 192.168.10.2      #网关
      netmask 255.255.255.0     #子网掩码
      ```

    + <img src="02_Linux%E4%B9%8BUbuntu.assets/image-20210112115917216.png" alt="image-20210112115917216"  />

+ 配置DNS

  + 进入文件 `vi /etc/systemd/resolved.conf`

  + 打开该文件找到 `#DNS=` 这一行把前面的 “#“ 去掉，然后在 “=”后面加上DNS服务器的地址

  + ````bash
    DNS=114.114.114.114 8.8.8.8
    ````

  + <img src="02_Linux%E4%B9%8BUbuntu.assets/image-20210112150057402.png" alt="image-20210112150057402" style="zoom:67%;" />

  + <img src="02_Linux%E4%B9%8BUbuntu.assets/image-20210112150307699.png" alt="image-20210112150307699" style="zoom:67%;" />

+ 重启虚拟机生效

  + `reboot`
  + `ip addr`或者`ifconfig`
  + `ping www.baidu.com`查看是否联网

#### 2.4.2 enp0s8

+ 17.10后，Ubuntu改成netplan方式 。

+ 打开文件`cd /etc/netplan/`

  + `ls`查看下面的文件，修改以`.yaml`后缀的文件，我这里是`01-netcfg.yaml`

  + ```bash
    network:
      version: 2
      renderer: networkd
      ethernets:
        ens33:   #配置的网卡名称
          dhcp4: no    #dhcp4关闭
          dhcp6: no    #dhcp6关闭
          addresses: [192.168.10.55/24, ]   #设置本机IP及掩码
          gateway4: 192.168.10.2   #设置网关
          nameservers:
              addresses: [114.114.114.114, 8.8.8.8]   #设置DNS
    ```

  + 注意`:`后有空格

  + `/24`子网掩码位数共32位，写24是前24个1，后8个0，相当于`255.255.255.0`，也相当于`11111111 11111111 11111111 10000000`

+ 保存后重启网络服务`netplan apply`

+ https://www.cnblogs.com/blueyunchao0618/p/11394640.html

## 3.Xshell连接Ubuntu

由于xshell远程连接ubuntu是通过ssh协议的，所以，确保ubuntu安装ssh服务器：

+ ```bash
  #安装远程ssh服务
  sudo apt-get install openssh-server
  #若没有ssh则安装
  sudo apt-get install ssh
  ```

## 4.问题

### 4.1 安装页面显示不全问题

安装时选择英文，不要中文，进去再改，否则出现页面中文适配导致页面显示不全。

+ <img src="C:%5CUsers%5CLenovo%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5Cimage-20210111190209640.png" alt="image-20210111190209640" style="zoom:50%;" />

### 4.2 vi编辑器异常

问题：方向键及backspace等异常

原因：安装的是vim.tiny版本，不是完整版

解决：

+ `sudo apt-get remove vim-commom`
+ `sudo apt-get install vim`

### 4.3 没有 ifconfig 命令

+ `sudo apt install net-tools`
+ 或者`sudo apt-get install net-tools`

