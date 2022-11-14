### 基本介绍

1. 日志文件是重要的系统信息文件，其中记录了许多重要的系统事件，包括用户登录信息、系统的启动信息、系统的安全信息、邮件相关信息、各种服务相关信息等。
2. 日志对于安全来说也非常重要，它记录了每天系统发生的各种事情，通过日志来检查错误发生的原因，或者受到攻击时攻击者留下的痕迹
3. 可以这样理解，日志是用来记录重大事件的工具。

### 系统常用的日志

- `/var/log/` 目录就是系统日志文件的保存位置

![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221114183538.png)

**常用系统日志如下：**
![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221114183719.png)
![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221114183901.png)

**示例**
用户通过 `MobaXterm` 或 `XShell` 等工具登录，使用了错误的密码，我们可以看看在日志文件 `/var/log/secure` 里有没有记录相关信息。

![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221114184441.png)

### 日志管理服务 `rsyslogd`

`CentOS7.6` 日志服务是 `rsyslogd`，`CentOS6.x` 日志服务是 `syslogd`，`rsyslogd` 功能更强大。
`rsyslogd` 的使用、日志文件的格式和 `syslogd` 服务是兼容的。

**查询 `Linux` 中的 `rsyslogd` 服务是否启动**
- `ps aux | grep "rsyslog" | grep -v "grep"` 
	- `grep -v` 反向匹配，只选择不匹配的行

**查询 `rsyslogd` 服务的自启动状态**
- `systemctl list-unit-files | grep rsyslog`

![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221114184831.png)

![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221114185109.png)

**配置文件：`/etc/rsyslog.conf`**
编辑文件时的格式为：`*.*` 存放日志文件，其中第一个`*`代表日志类型，第二个`*`代表日志级别
- 日志类型分为：
	- `auth`：`pam` 产生的日志
	- `authpriv`：`ssh`、`ftp` 等登录信息的验证信息
	- `corn`：时间任务相关
	- `kern`：内核
	- `lpr`：打印
	- `mail`：邮件
	- `mark(syslog)-rsyslog`：服务内部信息，时间标记
	- `news`：新闻组
	- `user`：用户程序产生的相关信息
	- `uucp`：`unix to nuix copy` 主机直接相关的通信
	- `local 1-7`：自定义的日志设备
- 日志级别分为：
	- `debug`：有调试信息的，日志通信最多
	- `info`：一般信息日志，最常用
	- `notice`：最具有重要性的普通条件的信息
	- `warning`：警告级别
	- `err`：错误级别，阻止某个功能或者模块不能正常工作的信息
	- `crit`：严重级别，阻止整个系统或者整个软件不能正常工作的信息
	- `alert`：需要立刻修改的信息
	- `emerg`：内核崩溃等重要信息
	- `none`：什么都不记录
	- 

![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221114185119.png)
**由日志服务 `rsyslogd` 记录的日志文件，其格式包含以下 4 列**

1. 事件产生的时间
2. 产生事件的服务器的主机名
3. 产生事件的服务器名或程序名
4. 事件的具体信息

**示例**
查看一下 `/var/log/secure` 日志，这个日志记录的是用户验证和授权方面的信息，分析如何查看
![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221114191308.png)

在 `/etc/rsyslog.conf` 中添加一个日志文件 `/var/log/rin.log` ，当有事件发生的时候（如 `sshd` 服务相关事件），该文件会接收到信息并保存。
![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221114191936.png)

```bash
# 增加自定义的日志
*.*                                                     /var/log/rin.log
```

![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221114191730.png)

![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221114192010.png)

### 日志轮替

**基本介绍**
日志轮替就是把旧的日志文件移动并改名，同时建立新的空日志文件，当旧日志文件超出保存的范围后，就会进行删除。

**日志轮替文件命名**

1. `CentOS7` 使用 `logrotate` 进行日志轮替管理，要想改变日志轮替文件名字，通过 `/etc/lograte.conf` 配置文件中 `dateext` 参数
2. 如果配置文件中有写 `dateext` 参数，那么日志会用日期来作为日志文件的后缀，例如 `secure-20271010`。这样日志文件名不会重叠，也就不需要日志文件的改名，只需要指定保存日志个数，删除多余的日志文件即可。
3. 如果配置文件中没有 `dateext` 参数，日志文件就需要进行改名了，当第一次进行日志轮替的时候，当前的 `secure` 日志会自动改名为 `secure.1`，然后新建 `secure` 日志，用来保存新的日志。当第二次进行日志轮替时 `secure.1` 会自动改名为 `secure.2`，当前的 `secure` 日志改名为 `secure.1`，然后也会新建 `secure` 日志用来保存新的日志。

#### **`logrotate` 配置文件**

`/etc/logrotate.conf` 是 `logrotate` 的全局配置文件

![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221114193533.png)

**参数说明**
![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221114193939.png)

#### 把自己的日志加入到日志轮替

1. 直接在 `/etc/logrotate.conf` 配置文件中写入该日志的轮替策略
2. 在 `/etc/logrotate.d/` 目录中新建该日志的轮替文件，在该轮替文件中写入轮替策略，因为该目录中的文件都会被 `include` 到主配置文件中，所有也可以把日志加入轮替。
3. 推荐使用方法二，因为系统中需要轮替的日志非常多，如果全部直接写入 `etc/logrotate.conf` 配置文件那么这个文件的可管理性就会非常差，不利于文件之后的维护。
4. `/etc/logrotate.d/` 配置轮替文件一览![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221114194501.png)
**示例**
在 `/etc/logrotate.conf` 进行配置，或者在 `/etc/logrotate.d/` 下创建文件 `rin` 编写如下内容，具体轮替效果可以参考 `/var/log` 下的 `boot.log`
```baah
/var/log/rin.log
{
	missingok
	daily
	copytruncate
	rotate 7
	notifempty
}
```
![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221114194944.png)

#### 日志轮替机制

日志轮替之所以可以在指定的时间备份日志，是依赖系统定时任务，在 `/etc/cron.daily/` 目录下就会发现这个目录中是有 `logrotate` 文件(可执行)，`logrotate` 通过这个文件去依赖定时任务执行的。
![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221114195326.png)


### 查看内存日志

**`journalctl` 可以查看内存日志，下面是常用的指令**

- `journalctl`：查看全部
- `journalctl -n 3`：查看最新3条
- `journalctl --since 19:00 -until 19:10:10`：查看起始时间到结束时间的日志可以加日期
- `journalctl -p err`：报错日志
- `journalctl -o verbose`：日志详细内容
- `journalctl _PID=123456 _COMM=sshd`：查看包含这些参数的日志（在详细日志查看）或者 `journalctl | grep sshd`

> `journalctl` 查看的是内存日志，重启会清空
![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221114200001.png)

