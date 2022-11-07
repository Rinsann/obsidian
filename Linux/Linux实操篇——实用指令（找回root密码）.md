### 指令运行级别

**基本介绍**
- 0：关机
- 1：单用户【找回丢失密码】
- 2：多用户状态没有网络服务
- 3：多用户状态有网络服务
- 4：系统未使用保留给用户
- 5：图形界面
- 6：系统重启
>常用运行级别是3 和 5，也可以指定默认运行级别

**例子：**
命令：`init [0123456]`  通过 `init` 来切换不同的运行级别，比如 5-3
```bash
init 3 # 从图形界面切换到命令行
init 5 # 从命令行切换回图形界面
```

**`CentOS7`以后版本运行级别说明**

在`centos 7` 之前，`/etc/inittab`文件中通过修改其中一行配置的数字修改的。
之后 `centos` 进行了简化，如下

```bash
multi-user.target: analogous to runlevel 3
graphical.target:analogous to runlevel 5
```

查看当前默认运行级别
```bash
systemctl get-default
```

设置默认运行级别
```bash
systemctl set-default multi-user.target
# 或者
systemctl set-default graphical.target
```
这样就可以改变运行级别了，改变后重启就直接进入 3 级别了。
![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221107155417.png)

### 如何找回root密码

- 假设 `root` 密码忘记了，如何找回密码呢
- 设置运行级别，`linux` 运行后，直接进入到命令行

1. 首先，启动系统，进入开机界面，在界面中按 `e`，进入编辑界面![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221107160033.png)
2. 进入编辑界面，使用键盘上的上下键把光标往下移动，找到以 `Linux16`开头的内容所在行数，在行的最后面输入：`init=/bin/sh`![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221107160522.png)
3. 接着，输入完成后直接按快捷键：`Ctrl+x` 进入单用户模式
4. 然后再光标闪烁的位置中输入：`mount -o remount,rw /` (注意空格)，完成后按回车![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221107160825.png)
5. 在新的一行最后输入：`passwd`，完成后按键盘的回车键，输入密码，然后再次确认密码即可，密码修改完成后，会显示 `passwd...`，说明密码修改成功。
6. 接着，在鼠标闪烁的位置输入：`touch /.autorelabel` (注意touch 与 / 后面有一个空格)，输入完按回车。
7. 继续在光标闪烁的位置输入：`exec /sbin/init` （注意空格），然后按回车等待系统自动修改密码（时间可能有点长，耐心等待），完成后系统会重启，新的密码就生效了。

### 帮助指令
> `Linux` 系统中隐藏文件是以 `.` 开头的文件

**`man` 获取帮助信息**
基本语法： `man` [命令或者配置文件] 
比如：查看 `ls` 命令的帮助信息 `man ls`
![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221107162332.png)

选项可以组合使用，比如 `ls -la` 还可以指定目录 `ls -la /home`
![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221107162618.png)

**`help` 指令**

基本语法： `help [命令]` 可以获得 `shell` 内置命令的帮助信息
![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221107162818.png)


### 文件目录类

**`pwd` 指令**
基本语法： `pwd`
描述：显示当前工作目录的绝对路径

**`ls` 指令**
基本语法：ls [选项]  [目录或文件]
常用选项
- -a : 显示当前目录的所有文件和目录，包括隐藏的
- -l：以列表的方式显示信息

