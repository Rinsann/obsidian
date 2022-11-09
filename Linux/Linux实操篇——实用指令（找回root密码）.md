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

**`cd` 指令**
基本语法：`cd [参数]` (功能描述：切换到指定目录)
`cd ~` 或者 `cd :` 回到自己的家目录，比如 `root`，`cd ~` 到 `/root`
`cd ..` 回到上一层目录
![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221108095615.png)

**`mkdir` 指令**
`mkdir` 指令用于创建目录
基本语法：`mkdir` [选项] 要创建的目录
常用选项
- -p：创建多级目录
![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221108095900.png)

**`rmdir` 指令**
`rmdir` 指令删除空目录，`remdir` 删除的是空目录，如果目录下有内容时无法删除。
基本语法：`rmdir` [选项] 要删除的空目录
>如果需要删除非空目录，需要使用 `rm -rf 要删除的目录`
![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221108100303.png)

**`touch` 指令**

`touch` 指令用于创建空文件
- 基本语法：`touch` 文件名称
![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221108100517.png)

**`cp`指令**
`cp` 指令是拷贝文件到指定目录
- 基本语法：`cp [选项] source dest`
- 常用选项：`-r` 用于递归复制整个文件夹
- 细节：强制覆盖并且不提示的方法：`\cp -r /home/bbb /opt/`
![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221108100906.png)
![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221108101133.png)

**`rm` 指令**
`rm` 指令用于移除文件或者目录
- 基本语法： `rm` [选项] 要删除的文件或目录
- 常用选项：
	- `-r`：递归删除整个文件夹
	- `-f`：强制删除不提示
- 细节：强制删除不提示的方法：带上 `-f` 参数即可

**`mv` 指令**
`mv` 用于移动文件和目录或者重命名
- 基本语法：
	- `mv oldNameFile newNameFile`  (重命名操作)
	- `mv /temp/movefile /targetFolder` (移动文件)
	- `mv pig.txt /root/cow.txt` (移动并且重命名)
	- `mv bbb/ /home/` (移动整个目录到`/home`下)

**`cat` 指令**
cat 指令用于查看文件内容
- 基本语法：cat [选项] 要查看的文件
- 常用选项：-n 显示行号
- `cat` 只能浏览文件不能修改文件，为了浏览方便，一般会带上管道命令 `| more` (管道命令把前面的结果交给下一个指令)
- `cat -n /etc/profile | more` ，回车下一行，空格翻页。
![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221108102744.png)

**`more` 指令**
`more` 指令是一个基于 VI 编辑器的文本过滤器，它以全屏的方式按页显示文本文件的内容，`more` 指令内置了很多快捷键。
- 基本语法： more 要查看的文件
![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221108103310.png)

**`less` 指令**
`less` 指令用来分屏查看文件内容，它的功能与 `more` 指令相似，但是比`more`指令更加强大，支持各种显示终端。
`less` 指令在显示文件内容时，并不是一次将整个文件加载之后才显示的，而是根据显示需要加载内容，对于显示大型文件具有较高的效率。
- 基本语法：`less` 要查看的文件

![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221108103832.png)

**`echo` 指令**
`echo` 指令用于输入内容到控制台
- 基本语法：echo [选项]  [输出内容]
- 输出环境变量![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221108133457.png)

**`head` 指令**
`head` 指令用于显示文本的开头部分内容，默认情况下 `head` 显示文件的前十行内容
- 基本语法：
	- head 文件（查看文件头10行内容）
	- head -n 5 文件名 （查看文件头5行内容，5可以是任意数字）

**`tail` 指令**
`tail` 用于输出文件中尾部的内容，默认情况下 `tail` 指令显示文件的最后10行内容。
- 基本语法：
	- tail 文件：用于查看文件尾部10行内容
	- tail -n 5 文件：用于查看文件最后5行内容，5可以是任意数字
	- tail -f  文件：实时追踪该文档的所有更新

**`>` 指令和 `>>` 指令**
`>` 输出重定向和 `>>` 追加
- 基本语法：
	- ls -l > 文件：列表的内容写入文件`a.txt`中（覆盖写）
	- ls -al >> 文件：列表的内容追加到文件 `aa.txt` 的末尾，指定文件不存在则会创建
	- cat 文件1 > 文件2：将文件1的内容覆盖到文件2
	- echo "内容" >> 文件：将内容追加到该文件
- ![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221108135306.png)
**`ln` 指令**
软链接也称为符号链接，类似于`windows`里的快捷方式，主要存放了链接其他文件的路径
- 基本语法：
	- `ln -s [原文件或目录] [软链接名]`：给原文件创建一个软链接
	- ![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221108140223.png)
	- `rm /home/myroot`：删除软链接，`myroot` 不要带斜杠，带上代表是目录
- 细节：当我们使用 `pwd` 查看目录时，仍然看到的是软链接所在的目录

**`history` 指令**
查看已经执行过的历史命令，也可执行历史命令
- 基本语法：
	- history ：查看所有的已经执行过的历史命令
	- history 10：查看最近十个执行过的命令
	- !+编号：![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221108140825.png)

### 时间日期类
**date指令**
- 显示当前日期基本语法
	1. date：显示当前时间
	2. date +%Y：显示当前年份
	3. date +%m：显示当前
	4. date +%d：显示当前是哪一天
	5. date "+%Y-%m-%d %H:%M:%S"：显示年月日时分秒
	6. ![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221108141504.png)
- 设置日期
	- date -s 字符串时间
	- `date -s "2020-11-03 20:01:10"`
	- 使用上面语法修改日期后可以通过 `hwclock -s`修改回来


**`cal` 指令**
查看日历指令 `cal`
- 基本语法
	- cal [选项]：不加选项，显示本月日历
	- `cal 2022`：显示整年的日历
- ![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221108142802.png)
### 搜索查找类

**find 指令**
find 指令将从指定目录向下递归地遍历其各个子目录，将满足条件的文件或者目录显示在终端。
- 基本语法
	- `find [搜索范围] [选项]`
	- 选项说明：
		- `-name`<查询方式>：按照指定的文件名查找模式查找文件![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221108143956.png)
		- `-user`<用户名>：查找属于指定用户名的所有文件![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221108144051.png)
		- `-size`<文件大小>：按照指定的文件大小查找文件（+n 大于 -n小于 n等于，单位还有k,M,G）![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221108144309.png)![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221108144513.png) `ls -lh` 加个`h`会将单位以更容易理解的方式显示。

**`locate` 指令**
`locate` 指令可以快速定位文件路径。`locate`指令利用事先建立的系统中的所有文件名称及路径的`locate`数据库实现快速定位给定的文件。`locate`指令无需遍历整个文件系统，查询速度较快，为了保证查询结果的准确度管理员必须定期更新`locate`时刻。
- 基本语法：
	- `locate` ：搜索文件
- 说明：由于`locate`指令基于数据库进行查询，所以第一次运行前，必须使用`updatedb`指令创建`locate`数据库
- ![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221108145138.png)
> `which` 指令，可以查看某个指令在那个目录下，比如ls在那个目录：`which ls`

**`grep` 指令和管道符号 `|`**
`grep` 过滤查找，管道符 `|`，表示将前一个命令的处理结果输出传递给后面的命令处理。
- 基本语法：
	- `grep` [选项] 查找内容 源文件
	- `cat /home/hello.txt | grep "yes"`![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221108145837.png)
	- `grep -n "yes" /home/hello.txt`
- 常用选项
	- `-n`：显示匹配行及行号
	- `-i`：忽略字母大小写

### 压缩和解压类
**`gzip/gunzip`** 指令
`gzip` 用于压缩文件，`gunzip` 用于解压。
- 基本语法：
	- `gzip` 文件名：压缩文件，只能将文件压缩为 `*.gz` 文件
	- `gunzip` 文件.gz：解压缩文件命令
- ![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221108153835.png)
**`zip/unzip` 指令**
`zip` 用于压缩多个文件（`gzip`只能压缩单个），`unzip` 用于解压，这个在项目中打包发布很有用
- 基本语法：
	- zip [选项] xxx.zip 将要压缩的内容：压缩文件和目录的命令
		- `zip -r myhome.zip /home/` 将`home`目录及其包含的子文件夹都进行压缩
	- unzip [选项] xxx.zip：解压缩文件
		- `mkdir /opt/tmp`
		- `unzip -d /opt/tmp /home/myhome.zip`
- zip 常用选项：
	- `-r`：递归压缩，即压缩目录
- unzip 常用选项：
	- `-d <目录>`：指定解压后文件的存放目录
![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221108154900.png)

**`tar` 指令**
`tar` 指令是打包指令，最后打包后的文件是 `.tar.gz` 的文件
- 基本语法：
	- `tar [选项] xxx.tar.gz 打包的内容`：打包目录，压缩后的文件格式`.tar.gz`
	- 压缩多个文件：`tar -zcvf pc.tar.gz /home/pig.txt /home/cat.txt`
	- 将文件夹成`.tar.gz`：`tar -zcvf myhome.tar.gz /home/`
	- 将 `pc.tar.gz` 解压到当前目录：
- 选项说明：
	- `-c`：产生`.tar`打包文件
	- `-v`：显示详细信息
	- `-f`：指定压缩后的文件名
	- `-z`：用 `gzip` 对文档进行压缩或解压，文件后缀`.gz`时压缩和解压都要加上![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221108160437.png)
	- `-x`：解包`
![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221108155901.png)
创建 `tmp2` 文件夹，通过`-C`（解压到指定位置）指定解压到`tmp2`目录下
![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221108160744.png)
