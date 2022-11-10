### `Linux` 组的基本介绍
在`Linux`中的每一个用户都必须属于一个组，不能独立于组外。在`Linux`中每个文件都有其**所有者、所在组、其它组**的概念。
1. 谁创建的文件，所有者就是谁
2. 文件属于那个组的，这个组的所有用户都对这个文件有一定权限
3. 其他的组，对这个文件也有不同的权限
![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221108164612.png)

### 文件/目录的所有者
一般为文件的创建者，谁创建了该文件，就自然成为该文件的所有者
- 查看文件的所有者
	- 指令：`ls -ahl`
	- 这个就是所有者![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221108164151.png)
- 修改文件的所有者
	- 指令：chown 用户名 文件名![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221108164332.png)

**组的创建**
基本指令：`groupadd` 组名
```bash
groupadd monster # 创建组
useradd -g monster fox # 创建用户并放入monster组
```
![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221108164554.png)
![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221108164900.png)

**修改文件所在的组**
基本指令：chgrp 组名 文件名
![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221108165255.png)

### 其他组
除文件的所有者和所在组的用户外，系统的其他用户都是文件的其他组

#### 改变用户所在组
在添加用户时，可以指定将该用户添加到那个组中，同样的用`root`的管理权限也可以改变某个用户所在的组。
**如何改变用户所在组**
1. usermod -g 新组名 用户名
2. usermod -d 目录名 用户名 (改变该用户登录的初始目录)。说明：修改后的目录用户需要有进入到该目录的权限。
![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221108165939.png)
### 权限的基本介绍
**ls -l 中显示的内容如下：**
`-rwxrw-r-- 1 root root 1213 Feb 2 09:39 abc`
**0-9 位说明**
1.  第0位确定文件类型（`d，-，l，c，b`）
	- `l` 是链接，相当于 `windows` 的快捷方式
	- `d` 是目录，相当于 `windows` 的文件夹
	- `c` 是**字符设备**文件，鼠标、键盘
	- `b` 是 块设备，比如硬盘
3. 第`1-3`位确定所有者（该文件的所有者）拥有该文件的权限。`---User`
4. 第`4-6`位确定所属组（同用户组的）拥有该文件的权限，`---Group`
5. 第`7-9`位确定其他用户拥有该文件的权限 `---Other`

### `rwx` 权限详解
**`rwx` 作用到文件**
1. [`r`]代表可读（`read`）：可以读取，查看
2. [`w`]代表可写（`write`）：可以修改，但是不代表可以删除该文件，删除一个文件的前提条件是对该文件所在的目录有写权限，才能删除该文件
3. [`x`]代表可执行（`execute`）：可以被执行
**`rwx` 作用到目录**
1. [`r`]代表可读（`read`）：可以读取，`ls` 查看目录内容
2. [`w`]代表可写（`write`）：可以修改，对目录内创建+删除+重命名文件
3. [`x`]代表可执行（`execute`）：可以将进入该目录

`Linux`系统中使用这10个字符确定不同用户能对文件做什么
- 第一个字符代表文件类型：- l d c b
- 其余字符每3个一组（`rwx`）：读（`r`）、写（`w`）、执行（`x`）
- 第一组`rwx`：文件拥有者的权限是读（`r`）、写（`w`）、执行（`x`）
- 第二组`rw-`：与文件拥有者同一组的用户的权限是读（`r`）、写（`w`）、但是不能执行
- 第三组`r--`：与文件拥有者不同组的其他用户的权限是能读，但是不能写和执行

> 可以使用数字表示为：`r=4,w=2,x=1` 因此 `rwx=4+2+1=7`

**其他说明**
- `1` ： 目录/链接个数，对于目录文件，表示它的第一级子目录的个数。注意此处看到的值要减2才等于该目录下的子目录的实际个数。虽然是空目录但是至少会有两个隐藏目录`.` 和 `..` ，分别表示当前目录和上层目录，所以会显示`2`![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221110120315.png)对于其他文件，表示指向它的链接文件的个数。
- `root`  ：用户
- `root` ：组
- `1213` ：文件大小（字节），如果是文件夹，显示 4096字节
- `Feb 2 09:39`： 最后修改日期
- `abc` ：文件名

### 修改权限-`chmod`
**基本说明：**
- 通过 `chmod` 指令，可以修改文件或者目录的权限
![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221110122741.png)

**第一种方式： `+、-、=` 变更取芯**
u：所有者，g：所有组，o：其他人，a：所有人(u/g/o的总和)
1. `chmod u=rwx,g=rx,o=x 文件/目录名`
2. `chmod o+w 文件/目录名`
3. `chmod a-x 文件/目录名`
4. `chmod u=rwx,g=rx,o=rx abc`：给`abc`文件的所有者读写执行的权限，给所在组读和执行权限，给其他组读和执行的权限。![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221110123254.png)当我们给文件执行的权限，他就变成了绿色的。
5. `chmod u-x,g+w abc`：给`abc`文件的所有者除去执行的权限，增加组写的权限![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221110123347.png)
6. `chmod a+r abc`：给所有用户添加 `abc` 添加文件读的权限![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221110123500.png)
**第二种方式：通过数字变更权限**
- `r=4,w=2,x=1`
- `rwx=4+2+1=7`
- `chmod 755 /home/abc.txt` 相当于给`/home/abc.txt`文件的权限修改为 `rwxr-xr-x`

### 修改文件所有者-`chown`
**基本介绍**
- chown newowner 文件/目录 改变所有者
- chown newowner:newgroup 文件/目录 改变所有者和所在组
- `-R` 如果是目录 则将其下所有子文件或目录递归生效

**示例**
![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221110124309.png)

- `chown rick /home/bbb/dd/abc.txt`![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221110124424.png)
- `chown -R rick /home/bbb/dd/test`![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221110124838.png)`test` 目录下的文件和目录也改变了![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221110124930.png)


### 修改文件/目录所在组-`chgrp`
**基本介绍：**
- `chgrp newgroup 文件/目录 改变所有组`
**示例：**
1. 将 `/home/bbb/dd/abc.txt` 文件的所在组修改成 `shaolin`
```bash
groupadd shaolin
chgrp shaolin /home/abc.txt
```
![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221110125405.png)
2. 将 `/home/bbb/dd/test` 目录下的所有文件和目录的所在组都修改成 `shaolin`
```bash
chgrp -R shaolin /home/bbb/dd/test
```
![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221110125639.png)
![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221110125653.png)

### 实践-警察和土匪
police，bandit
jack，jerry：警察
xh，xq：土匪
1. 创建组 `groupadd police;groupadd bandit`
2. 创建用户 `useradd -g police jack; useradd -g police jerry;useradd -g bandit xh;useradd -g bandit xq;`
3. `jerry` 创建一个文件，自己可以读写，本组可以读，其他组没有任何权限
	- `jerry` 登录；`vim java.txt`；`chmod 640 jack.txt`
4. `jack` 修改该文件，让其他组可以读，本组可以读写
	- `chmod 664 java.txt`
5. `xh` 投靠警察，看看是否可以读写
	- `usermod -g polic xh`
6. `xh` 是否可以读写，`xq` 是否可以读写
	- 如果要对目录类的文件进行操作，还需要有对该目录的相应权限
	- c`hmod 770 /home/jerry/`
