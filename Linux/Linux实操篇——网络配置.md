### Linux 网络配置原理图
![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221111154849.png)

### 查看网络`IP`和网关

**查看虚拟网络编辑器和修改`IP`地址**
![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221111160633.png)
**查看网关**
![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221111160744.png)

查看 `windows` 环境中的 `vmnet8` 网络配置（`ipconfig` 指令）
![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221111160927.png)

查看 `Linux` 的配置 `ifconfig`
![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221111160908.png)

### Linux 网络环境配置

**第一种方式（自动获取）**
说明：登录后，通过界面来设置自动获取 `ip`，特点是 `Linux` 启动后会自动去获取 `IP` 地址，缺点是每次自动获取的 `IP` 地址可能不一样。
![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221111161538.png)

**第二种方法（指定`ip`）**
说明：
- 直接修改配置文件来指定 IP，并可以连接到外网
- 编辑 `vim /etc/sysconfig/network-scripts/ifcfg-ens33`
- 要求：将 `ip` 地址配置静态的，比如：`ip` 地址为 192.168.200.130
![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221111162534.png)

**`ifcfg-ens33` 文件说明**
- `DEVICE=eth0`    #   接口名（设备，网卡）
- `HWADDR=00:0C:2x:6x:0x:xx`    # MAC 地址
- `TYPE=Ethernet`    # 网络类型
- `UUID=`    # 随机 ID
- `ONBOOT=yes`     # 系统启动的时候网络接口是否有效（yes/no）
- `BOOTPROTO=static`    #  IP的配置方法`[none|static|bootp|dhcp]` (引导时不使用协议|静态分配IP|BOOTP协议|DHCP协议)
- `IPADDR=192.168.200.130`    # IP 地址
- `GATEWAY=192.168.200.2`    #  网关
- `DNS1=192.168.200.2`    # 域名解析器
![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221111162827.png)
然后修改 `VMware` 虚拟机网络设置
![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221111163040.png)
**最后重启网络或者重启系统即可生效**
```bash
service network restart
# 或者
reboot
```
![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221111163315.png)
![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221111163336.png)
可以 `ping` 通 `Linux` 系统
![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221111163454.png)

![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221111163227.png)

### 设置主机名和 `hosts` 映射

**设置主机名**
1. 主要是为了方便记忆，可以给 `Linux` 系统设置主机名，也可以根据需要修改主机名
2. 指令 `hostname`：查看主机名
3. 修改文件在 `/etc/hostname` 中指定![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221111163945.png)
4. 修改后，重启即可生效

**设置 `hosts` 映射**
`windows`系统在 `C:\Windows\System32\drivers\etc\hosts` 文件中指定即可
![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221111170600.png)
![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221111170744.png)![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221111170902.png)

`Linux` 系统则在 `/etc/hosts` 文件中指定
![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221111171303.png)
![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221111171311.png)

### 主机名解析过程分析（Hosts、DNS）
**`Hosts` 是什么**
- 一个文本文件，用来记录 `IP` 和 `Hostname`（主机名）的映射关系

`DNS`
1. `DNS`，就是 `Domain Name System` 的缩写，翻译过来就是域名系统
2. 是互联网上作为域名和 `IP` 地址互相映射的一个分布式数据库

**举个例子**
用户在浏览器中输入了 www.baidu.con
1. 浏览器先检查浏览器缓存中有没有该域名的解析 `IP` 地址，有就先调用这个 `IP`完成解析；如果没有就检查操作系统的 `DNS` 解析器缓存，有就直接返回 `IP` 完成解析。这两个缓存，可以理解为 本地解析器缓存
2. 一般来说，当电脑第一次成功访问某一网站后，在一定时间内，浏览器或操作系统会缓存它的`IP` 地址（`DNS` 解析记录），可以在 `cmd` 窗口中输入 `ipconfig /displaydns` 它是  `DNS` 域名解析缓存 或者 `ipconfig /flushdns` 手动清理 `dns` 缓存
3. 如果本地解析器缓存没有找到对应映射，再检查系统中 `hosts` 文件有又没有对应配置的域名 `IP` 映射，如果有，则完成解析并返回
4. 如果本地 `DNS` 解析器缓存和 `hosts` 文件中均没有找到对应 `IP`，则到域名服务 `DNS` 进行域解析

![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221111173801.png)
