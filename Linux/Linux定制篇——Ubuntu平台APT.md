### APT原理机制

![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221114145040.png)

### Ubuntu 软件操作的相关命令
- `sudo apt-get update`：更新源
-  `sudo apt-get install package`：安装包
-  `sudo apt-get remove package`：删除包
-  `sudo apt-cache search package`：搜索软件包
-  `sudo apt-cache show package`：获取包的信息，如：说明、大小、版本等
-  `sudo apt-get install package --reinstall`：重新安装包
-  `sudo apt-get -f install`：修复安装
-  `sudo apt-get remove package --purge`：删除包，包括配置文件
-  `sudo apt-get build-dep package`：安装相关的编译环境
-  `sudo apt-get upgrade`：更新已安装的包
-  `sudo apt-get dist-upgrade`：升级系统
-  `sudo apt-cache depends package`：了解使用该包依赖了那些包
- `sudo apt-cache rdepends package`：查看该包被那些包依赖
- `sudo apt-get source package`：下载该包的源代码

### 更新 Ubuntu 软件下载地址
![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221114150121.png)

**原理图**


**寻找国内镜像源**
清华镜像：https://mirrors.tuna.tsinghua.edu.cn/
清华Ubuntu：https://mirrors.tuna.tsinghua.edu.cn/help/ubuntu/
所谓的镜像源，可以理解为提供下载软件的地方，比如 `Android` 手机上可以下载软件的安卓市场，IOS 手机可以下载软件的 `AppStore`

**备份 `Ubuntu` 默认的源地址**
```bash
sudo cp /etc/apt/sources.list /etc/apt/sources.list.back
```
![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221114150423.png)

**更新源服务器列表**
先情况 `source.list` 文件并复制镜像网站的地址
```bash
su root
echo '' > sources.list

vim sources.list

# 粘贴

# 默认注释了源码镜像以提高 apt update 速度，如有需要可自行取消注释
deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ focal main restricted universe multiverse
# deb-src https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ focal main restricted universe multiverse
deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ focal-updates main restricted universe multiverse
# deb-src https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ focal-updates main restricted universe multiverse
deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ focal-backports main restricted universe multiverse
# deb-src https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ focal-backports main restricted universe multiverse
deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ focal-security main restricted universe multiverse
# deb-src https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ focal-security main restricted universe multiverse

# 预发布软件源，不建议启用
# deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ focal-proposed main restricted universe multiverse
# deb-src https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ focal-proposed main restricted universe multiverse
```

![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221114150559.png)
![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221114150954.png)

**更新源地址**

```bash
sudo apt-get update
```
![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221114151433.png)

### Ubuntu 软件安装，卸载

**示例**
- 使用 apt 安装和卸载 vim 软件，并查询 vim 的信息

```bash
sudo apt-get remove vim # 删除
sudo apt-get install vim # 安装
sudo apt-cache show vim # 获取软件信息
```
![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221114151651.png)
![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221114151745.png)

# 远程登录 Ubuntu

### SSH 介绍

`SSH` 为 `Secure Shell` 的缩写，由 `IETF` 的网络小组所制定，`SSH` 为建立在应用层和传输层基础上的安全协议。

`SSH` 是目前较可靠，专门为远程登录会话和其他网络服务提供安全性的协议，几乎所有 `UNIX/Linux` 平台都可以运行 `SSH`。

使用 `SSH` 服务，需要安装相应的服务器和客户端，客户端和服务器的关系如：`A` 机器想被 `B` 机器远程控制，那么，`A` 机器需要安装 `SSH` 服务器，`B` 机器需要安装 `SSH` 客户端。

和 `CentOS` 不一样，`Ubuntu` 默认没有安装 `SSHD` 服务（使用 `netstat -anp` 指令查看，`apt install net-tools`），因此不能直接进行远程登录，需要先安装 `SSHD`
![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221114152959.png)

### SSH 远程登录示意图

![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221114153036.png)

### 安装 SSH 和启用

```bash
sudo apt-get install openssh-server
```

执行上面指令后就在当前这台 `Linux` 上安装了 `SSH` 服务端和客户端

```bash
service sshd restart
```

执行这条指令，启动 `sshd` 服务，并且会自动监听 `22` 端口
![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221114153444.png)

#### 从一台 `Linux` 系统远程登录到另一台 `Linux` 系统
![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221114153949.png)

**在创建服务器集群时，会使用到该技术**

- `ssh` 用户名@IP
	- 例如：`ssh rinsan@192.168.200.130`
- 使用 `ssh` 访问，如访问出错，可以查看是否有该文件 `~/.ssh/known_ssh` 尝试删除该文件解决。
登出命令：`exit` 或者 `logout`

