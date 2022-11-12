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
- 当我们执行一个 `shell` 脚本时，希望获取到命令行的参数信息，就可以使用到未知参数变量
- 比如：`./myshell.sh 100 200`，这个就是一个执行 `shell` 的命令行，可以在 `myshell` 脚本中获取到参数信息

**基本语法**
- `$n`：`n` 为数字，`$0` 代表命令本身，`$1-$9` 代表第一个到第九个参数，十以上的参数需要用大括号抱起来 （如 `${10}`）
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
