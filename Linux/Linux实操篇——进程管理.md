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
- 踢出某个非法登录用户
- 终止远程登录服务 `sshd`，在适当的时候再次重启 `sshd` 服务
- 终止多个 `gedit`
- 强制杀掉一个终端