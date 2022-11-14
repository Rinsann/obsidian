### 为什么要学习 `Shell` 编程
1. `Linux` 运维工程师在进行服务器集群管理时，需要编写 Shell 程序来进行服务器管理
2. 对于 `JavaEE` 和 `Python` 程序员来说，工作的需要使用 `Shell` 脚本进行程序或者服务器的维护，比如编写一个定时备份数据库的脚本
3. 对于大数据程序员来说，需要编写 Shell 脚本用于管理集群

### `Shell` 是什么
- Shell 是一个命令行解释器，它为用户提供了一个向 Linux 内核发送请求以便运行程序的界面系统级程序，用户可以用 Shell 来启动、挂起、停止甚至编写一些更复杂的程序。
![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221112220710.png)

### `Shell` 脚本的执行方式
**脚本格式要求**
1. 脚本以 `#!/bin/bash` 开头
2. 脚本需要有可执行权限
**编写第一个 `Shell` 脚本**
- 创建一个 `Shell` 脚本，输出 Hello World!
**脚本常用执行方式**
1. 输入脚本的绝对路径或相对路径（首先要赋予脚本的 `+x` 权限，在执行脚本）![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221112221735.png)
2. `sh` + 脚本，不用赋予脚本 `+x` 权限直接执行即可![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221112221856.png)
```bash
#!/bin/bash
echo "Hello World!"
```

### `Shell` 的变量

**`Shell` 变量介绍**
1. `Linux Shell` 中的变量分为，系统变量和用户自定义变量。
2. 系统变量：`$HOME/$PWD/$SHELL/$USER` 等等，比如：`echo $HOME`
3. 显示当前 `shell` 中的所有变量：`set`
![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221112222452.png)

**`Shell` 变量的定义**
- 定义变量：变量=值
- 撤销变量：unset 变量
- 声明静态变量：readonly 变量（不能 `unset`）

**示例**
```bash
#!/bin/bash

# 定义变量
A=100

# 输出变量需要加上$
echo $A
echo A=$A
echo "A=$A"

# 撤销变量
unset A
echo "A=$A"

# 声明静态变量
readonly B=2
echo "B=$B"

unset B

```

![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221112222928.png)

**定义变量的规则**
1. 变量名称可以由字母、数字和下划线组成，但是不能以数字开头
2. 等号两侧不能有空格
3. 变量名称一般习惯大写，这是一个规范。

**将命令的返回值赋值给变量**
```bash
C=`date` # 反引号，运行里面的命令，并把结果返回给变量A
D=$(date) # 等价于反引号

echo C=$C
echo "D=$D"
```

![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221112223734.png)

### 设置环境变量

**基本语法**
- 将 `shell` 变量输出为环境变量/全局变量：export 变量名=变量值
- 让修改后的配置立即生效：source 配置文件、
- 查询环境变量的值：echo $变量名

**示例**
1. 在 `/etc/profile` 文件中定义 `TOMCAT_HOME` 环境变量
2. 查看环境变量 `TOMCAT_HOME` 的值
3. 在另一个 `shell` 程序中使用 `TOMCAT_HOME`
4. shell 脚本的多行注释：`:<<! 内容 !`
```bash
# 使用环境变量 TOMCAT_HOME
echo "tomcat_home=$TOMCAT_HOME"

:<<!
注意换行，这里是多行注释
C=`date`
D=$(date)
echo C=$C
echo "D=$D"
!
```
![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221112224713.png)


>注意：在输出  `TOMCAT_HOME`  环境变量前，需要让其生效 `source /etc/profile`

### 位置参数变量
**介绍**
- 当我们执行一个 `shell` 脚本时，希望获取到命令行的参数信息，就可以使用到位置参数变量
- 比如：`./myshell.sh 100 200`，这个就是一个执行 `shell` 的命令行，可以在 `myshell` 脚本中获取到参数信息

**基本语法**
- `$n`：`n` 为数字，`$0` 代表命令本身，`$1-$9` 代表第一个到第九个参数，十以上的参数需要用大括号包起来 （如 `${10}`）
- `$*`：这个变量代表命令行中所有的参数，`$*` 把所有的参数看做一个整体
- `$@`：这个变量也代表命令行中所有的参数，不过`$@` 把每个参数区分对待
- `$#`：这个变量代表命令行中所有参数的个数

**位置参数变量示例**
- 编写一个 `shell` 脚本 `position.sh` ，在脚本中获取到命令行的各个参数信息
![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221112230326.png)
```bash
#!/bin/bash
echo "0=$0 1=$1 2=$2"
echo "所有的参数=$*"
echo "$@"
echo "参数的个数=$#"
```

### 预定义变量
**基本介绍**
- 就是 `shell` 设计者事先定义好的变量，可以直接在 `shell` 脚本中使用

**基本语法**
- `$$`：当前进程的进程号（`PID`）
- `$!`：后台运行的最后一个进程的进程号（`PID`）
- `$?`：最后一次执行的命令的返回状态，如果这个变量的值为0，证明上一个命令正常执行；如果这个变量的值为非 0（具体那个数，由命令自己来决定），则证明上一个命令执行不正确看。

**示例**
```bash
#!/bin/bash
echo "当前执行的进程id=$$"

# 已后台的方式运行一个脚本，并获取它的进程号
/root/shcode/myshell.sh &
echo "最后一个后台运行的进程id=$!"
echo "执行的结果是=$?"
```
![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221113180423.png)

### 运算符
**基本介绍**
- 用于在 `Shell` 中进行各种运算操作

**基本语法**
1. `$((运算公式))` 或者 `$[运算公式]` 还有 `expr m + n`
2. `expr m -n` ：m 和 n 之间需要有空格，(`expr` 是 `expression` 简写)
3. 如果希望将 expr 的结果赋值给某个变量需要使用反引号  ``
4. `expr \*,/,%`：乘、除、取余
```bash
#!/bin/bash
# 计算 (2+3)*4的值

RES1=$(((2+3)*4))
echo "res1=$RES1"
RES2=$[(2+3)*4]
echo "res2=$RES2"
TEMP=`expr 2 + 3`
RES4=`expr $TEMP \* 4`
echo "temp=$TEMP"
echo "res4=$RES4"

# 请输出命令行的两个参数[整数]的和 20 50
SUM=$[$1+$2]
echo "sum=$SUM"
```
![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221113181834.png)

### 条件判断
**判断语句基本语法**
- [ condition ] ：注意 `condition` 前后要有空格 即使里面什么都没有也需要空格，非空返回 true，可使用 `$?` 验证（0为 True，>1 为 False）

**示例**
- [ Rinsan ]         # 返回 true
- [  ]                          # 返回 false
- `[ condition] && echo OK || echo notok`               条件满足执行后面的语句

**常用判断条件**
1. `=` 字符串比较
2. 两个整数的比较
	-  `-lt` 小于
	-  `-le` 小于等于
	-  `-eq` 等于
	-  `-gt` 大于
	-  `-ge` 大于等于
	-  `-ne` 不等于
3. 按照文件权限进行判断
	- `-r` 有读的权限
	- `-w` 有写的权限
	- `-x` 有执行的权限
4. 按照文件类型进行判断
	- `-f`  文件存在并且是一个常规的文件
	- `-e`  文件存在
	- `-d`  文件存在并且是一个目录

**示例**

```bash
#!/bin/bash

if [ "ok" = "ok" ]
then
    echo "equal"
fi

if [ 23 -ge 22 ]
then
    echo "大于"
fi

if [ -f /root/shcode/aaa.txt ]
then
    echo "文件存在"
fi

```
![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221114103845.png)

### 流程控制

**`if` 判断基本语法**
```bash
if [ 条件判断表达式 ]
then
    代码
fi
# 或者
if [ 条件判断表达式 ]
then
    代码
elif  [ 条件判断表达式 ]
then
    代码
fi
```
>[ 条件判断表达式 ] 中括号和条件判断表达式之间必须有空格

**示例**
```bash
#!/bin/bash
if [ $1 -ge 60 ]
then
	echo "及格了"
elif [ $1 -lt 60 ]
then
	echo "不及格"
fi
```

![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221114104107.png)

**`case` 语句基本语法**
```bahs
case $变量名 in 
"值1") # 如果变量的值等于值1，则执行程序1
;;
"值2") # 如果变量的值等于值2，则执行程序2
;;
...
*) # 如果变量的值不是以上的值，则执行此程序
;;
esac
```

**示例**
```bash
#!/bin/bash
case $1 in
"1")
echo "周一"
;;
"2")
echo "周二"
;;
*)
echo "other..."
esac
```
![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221114104822.png)

**`for` 循环基本语法**
```bash
# 语法1
for 变量 in 值1 值2 值3 ...
do
程序
done

# 语法2
for (( 初始值;循环控制条件;变量变化))
do
程序
done
```

**示例**
`vim testFor1.sh`
```bash
#!/bin/bash
# "$*" 是把所有的参数当作一个整体，所以只会输出一句话
for i in "$*"
do
        echo "num is $i"
done

# 使用 $@ 来获取输入的参数，注意 $@ 是分别对待，所以有几个参数就输出几句
echo "================================================="
for j in "$@"
do
	echo "num is $j"
done
```

![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221114112607.png)![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221114112836.png)
`vim testFor2.sh`
```bash
#!/bin/bash
# 从1加到100的值输出显示，将100 做成一个变量
SUM=0
for(( i=1; i<=$1; i++))
do
        SUM=$[$SUM+$i]
done
echo "总和SUM=$SUM"
```
![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221114113754.png)
**`while` 循环基本语法**
```bash
while [条件判断表达式]
do
程序
done
```

**示例**
```bash
#!/bin/bash
# 从命令行输入一个数字 n，统计从1+—...+n的值是多少
SUM=0
i=0
while [ $i -le $1 ]
do
        SUM=$[$SUM+$i]
        # i 自增
        i=$[$i+1]
done
echo "执行结果=$SUM"
```
![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221114114320.png)

### `read` 读取控制台输入

**基本语法**
- `read [选项] [参数]`
- 选项：
	- `-p`：指定读取值时的提示符
	- `-t`：指定读取值时等待的时间（秒），如果没有在指定的时间内输入，就不用等待了
- 参数
	- 变量：指定读取值的变量名

**示例**
```bash
#!/bin/bash
#!/bin/bash
# 读取控制台输入一个 NUM1 的值
read -p "请输入一个数字NUM1=" NUM1
echo "输入的NUM1=$NUM1"

# 读取控制台输入一个NUM2的值，在10秒之内
read -t 10 -p "请输入一个数字NUM2=" NUM2
echo "输入的NUM2=$NUM2"
```
![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221114115013.png)

### 函数

**函数介绍**
- Shell 编程和其他编程语言语言，有系统函数，也可以自定义函数。

#### 系统函数
- `basename`基本语法：用于返回完整路径最后 `/` 的部分，常用于获取文件名
	- `basename [pathname] [suffix]`
	- `basename [string] [suffix]` : `basename` 命令会删掉所有的前缀包括最后一个 `/` 字符，然后将字符串显示出来
	- 选项：
	- `suffix` 为后缀，如果 `suffix` 被指定了，`basename` 会将 `pathname` 或 `string` 中的 `suffix` 去掉
- `dirname` 基本语法：用于返回完整路径最后 `/` 的前面部分，常用于返回路径部分
	- `dirname` 文件绝对路径：从给定的包含绝对路径的文件名中去除文件名（非目录的部分），然后返回剩下的路径（目录部分）

**示例**
```bash
basename /home/apple.txt
basename /home/apple.txt .txt

dirname /home/bbb/hello.txt
dirname /home/bbb/dd/hello.txt
```
![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221114115726.png)
![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221114120204.png)

#### 自定义函数

**基本语法**
```bash
[ function ] funname[()]
{
	Action;
	[return int;]
}

调用直接写函数名：funname [值]
```

**示例**
计算输入的两个参数之和（动态获取），`getSum`
```bash
#!/bin/bash

function getSum() {
        SUM=$[$n1+$n2]
        echo "和是=$SUM"
}

read -p "请输入n1=" n1
read -p "请输入n2=" n2

getSum $n1 $n2
```
![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221114120921.png)

### `Shell` 编程综合案例——备份数据库

**需求分析**
1. 每天凌晨 `2:30` 备份数据库 `rinsan` 到 `/data/backup/db`
2. 备份开始和备份结束能够给出相应的提示信息
3. 备份后的文件要求以备份时间为文件名，并打包成 `.tar.gz`，比如：`2027-03-13_023001.tar.gz`
4. 在备份的同时，检查是否有10天前备份的数据库文件，如果有就将其删除。
![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221114122253.png)
```bash
#!/bin/bash
echo "开始备份数据库 `date`"
# 备份目录
BACKUP=/data/backup/db
# 当前时间
DATETIME=$(date +%Y-%m-%d_%H%M%S)
echo "$DATETIME"
# 数据库的地址
HOST=localhost
# 数据库用户名
DB_USER=root
DB_PW=12345678
# 备份的数据库
DATABASE=rinsan

# 创建备份目录 如果不存在就创建
[ ! -d "${BACKUP}/${DATETIME}" ] && mkdir -p "${BACKUP}/${DATETIME}"

# 备份数据库
mysqldump -u${DB_USER} -p${DB_PW} --host=${HOST} -q -R --databases ${DATABASE} | gzip > ${BACKUP}/${DATETIME}/$DATETIME.sql.gz

# 将文件处理成 tar.gz
cd ${BACKUP}
tar -zcvf $DATETIME.tar.gz ${DATETIME}
# 删除对应的备份目录
rm -rf ${BACKUP}/${DATETIME}

# 删除十天前的备份文件
find ${BACKUP} -atime +10 -name "*.tar.gz" -exec rm -rf {} \;
echo "备份数据库---- ${DATABASE} ----成功"
```

> `-atime` 读取时间，`-mtime` 修改时间，`-ctime` 创建时间

![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221114133445.png)
