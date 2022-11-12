### 基本介绍
1. 在 `Linux` 中，每个执行的程序都称为一个进程，每个进程都分配一个 `ID` 号（`pid`，进程号）=>windows=>Linux![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221111184718.png)
2. 每个进程可能以两种方式存在，前台和后台，所谓前台进程就是用户目前屏幕上可以操作的，后台进程则是实际上在操作的，但由于屏幕上没有显示到的进程，通常使用后台方式在执行。
3. 一般系统的服务都是以后台进程的方式存在，而且都会常驻在系统中，直到关机才会结束。
### 显示系统执行的进程
**基本介绍**
- `ps` 指令：用来查看目前系统中，有哪些正在执行的进程，以及它们执行的状况，可以不加任何参数![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221111190411.png)
**可选参数**
- `-a`：显示当前终端的所有进程信息
- `-u`：以用户的格式显示进程信息
- `-x`：显示后台进程运行的参数
![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221111185630.png)

![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221111190355.png)

**`ps` 详解**
1. 指令：`ps -aux | grep sshd`，比如看看有没有 `sshd` 服务![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221111191041.png)
2. 指令说明
	- `System V` 展示风格
	- `USER`：用户名称
	- `PID`：进程号
	- `%CPU`：进程占用 `CPU` 的百分比
	- `%MEM`：进程占用物理内存的百分比
	- `VSZ`：进程占用虚拟内存大小（单位：`KB`）
	- `RSS`：进程占用的物理内存大小（单位：`KB`）
	- `TTY`：终端名称，缩写
	- `STAT`：进程状态，其中 `S-` 睡眠，`s-` 表示该进程是会话的先导进程，`N-` 表示进程拥有比普通优先级更低的优先级，`R-` 正在运行，`D-` 短期等待，`Z-` 僵死进程，`T-` 被跟踪或者被停止等等
	- `STARTED`：进程的启动时间
	- `TIME`：`CPU` 时间，即进程使用 `CPU` 的总时间
	- `COMMAND`：启动进程所用的命令和参数，如果过长会被截断显示

### 父子进程管理
**以全格式显示当前所有的进程，查看进程的父进程**
比如查看 `sshd` 的父进程信息
- `ps -ef`：是以全格式显示当前所有的进程
- `-e` 显示所有进程，`-f` 全格式
	- `-e` 显示所有进程，不管有没有被执行
	- `-a` 是显示当前终端执行的所有进程
- `ps -ef | grep sshd` 是 `BSD` 风格![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221112104436.png)
- `UID`：用户 `ID`
- `PID`：进程 `ID`
- `PPID`：父进程 `ID`
- `C`：`CPU` 用于计算机执行优先级的因子，数值越大，表明进程是  CPU `密集型运算`，执行优先级会降低；数值越小表明进程是 `I/O` 密集型计算，执行优先级会提高
- `STIME`：进程启动的时间
- `TTY`：完整的终端名称
- `TIME`：`CPU` 时间
- `CMD`：启动进程所使用的命令和参数

### 终止进程 `kill` 和 `killall`

**介绍**
若是某个进程执行一半需要停止时，或是已经消耗了很大的系统资源考虑停止该进程可以使用 `kill` 命令完成此项任务

**基本语法**
- `kill` [选项] 进程号：通过进程号杀死进程
- `killall` 进程名称：通过进程名称杀死进程，也支持通配符，这在系统因负载过大而变得缓慢时有用。

**常用选项**
- `-9`：表示强迫进程立即停止

**示例**
- 踢出某个非法登录用户 `kill 进程号`
- 终止远程登录服务 `sshd`，在适当的时候再次重启 `sshd` 服务![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221112113928.png)重启 `sshd` 服务：`/bin/systemctl start sshd.service`![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221112114110.png)
- 终止多个 `gedit` ，直接关闭打开的文本编辑器进程![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221112114254.png)
- 强制杀掉一个终端，`kill -9 bash 进程号` ![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221112114602.png)
### 查看进程树 `pstree`

**基本语法**
- `pstree [选项]` ：可以更加直观的以树状形式来查看进程信息
![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221112114923.png)

**常用选项**
- `-p`：显示进程的 `PID`![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221112115009.png)

- `-u`：显示进程的所属用户

### 服务（`service`）管理
**介绍**
服务（`service`）本质就是进程，但是它是运行在后台的，通常都会监听某个端口，等待其它程序的请求。比如（`mysqld`、`sshd` 防火墙等），因此又称为守护进程，是 `Linux` 中非常重要的知识
![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221112120002.png)

**`service` 管理指令**
1. `service` 服务名 `[start | stop | restart | reload | status]`
2. 在 `CentOS7` 后 很多服务不再使用 `service`，而是 `systemctl` 
3. 目前`service` 指令还管理的服务在 `/etc/init.d` 中查看![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221112120154.png)

`service` 管理指令示例
![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221112120524.png)

**查看服务名**
1. 使用 `setup` -> 系统服务 就能看到全部![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221112120649.png)
2. `/etc/init.d` 看到 `service` 指令管理的服务![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221112120853.png)按 `tab` 键可以跳到最下面选择退出即可

**开机的流程说明**
![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221112121012.png)

**`chkconfig` 指令**
1. 通过 `chkconfig` 目录可以给服务的各个运行级别设置自启动/关闭
2. `chkconfig` 指令管理的服务在 `/etc/init.d` 查看

**`chkconfig` 基本语法**
- 查看服务：`chkconfig --list [| grep xxx]`![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221112135455.png)
- `chkconfig 服务名 --list`
- `chkconfig --level 5 服务名 on/off`![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221112135642.png)

>使用 `chkconfig` 重新设置服务自启动/关闭，需要重启机器(`reboot`)才能生效

### `systemctl` 管理指令
1. 基本语法：
	- `systemctl [start | stop | restart | status] 服务名`
2. `systemctl` 指令管理的服务在 `/usr/lib/systemd/system` 查看

**`systemctl` 设置服务的自启动状态**
1. `systemctl list-unit-files [ | grep 服务名]`：查看服务开机启动状态，`grep` 可以进行过滤 ![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221112140515.png)
2. `systemctl enable 服务名`：设置服务开机启动
3. `systemctl disable 服务名`：关闭服务开机启动
4. `systemctl is-enabled 服务名`：查询某个服务是否是自启动的

**示例：**
`systemctl status firewalld`：查询防火墙当前状态![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221112140823.png)`systemctl stop firewalld`：关闭防火墙


**细节**
1. 关闭或者启用防火墙后，立即生效。 `cmd` 测试 `telnet 测试 某个端口即可` ，要在`windows`中打开这个功能。
2. 这种方式只是临时生效，当重启系统后，还是回归以前对服务的设置
3. 如果设置某个服务器自启动或者关闭，希望它永久生效，要使用 `systemctl [enable|disable] 服务名`
![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221112145913.png)

**打开或者关闭指定端口**
生产环境，往往需要将防火墙打开，但是问题来了，如果我们把防火墙打开，那么外部请求数据包就不能跟服务器监听端口通讯。
这时就需要打开指定的端口，比如：80/22/8080等。

**`firewall` 指令**
- 打开端口：`firewall-cmd --permanent --add-port=端口号/协议`
- 关闭端口：`firewall-cmd --permanent --remove-port=端口号/协议`
- 重新载入，才能生效：`firewall-cmd --reload`
- 查询端口是否开放：`firewall-cmd --query-port=端口/协议`
![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221112142935.png)


### 动态监控进程
**介绍**
`top` 和 `ps` 命令很相似，它们都是用来显示正在执行的进程。`top` 与 `ps` 最大的不同之处在于 `top` 在执行过程可以更新正在运行的进程
**基本语法**
`top [选项]`

![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221112143220.png)
![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221112143839.png)
![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221112144359.png)

**交互操作说明**
![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221112144727.png)

**示例**
比如：监控特定用户 `jack`
输入 top 按回车键查看执行的进程，然后输入 u 回车，在输入用户名即可。
![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221112145023.png)

![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221112144943.png)
终止指定的进程，比如要结束 `jack` 的登录
![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221112145315.png)
![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221112145323.png)

指定系统状态更新的时间（每10秒自动更新），默认3秒
`top -d 10`![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221112145447.png)

### 监控网络状态

**查看系统网络情况 `netstat`**

基本语法：`netstat [选项]`
选项说明
- `-an`：按一定顺序排列输出
- `-p`：显示那个进程在调用

![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221112150510.png)
![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221112150614.png)
