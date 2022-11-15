## 基本介绍

实体机无法做快照，如果系统出现异常或者数据损坏，后果严重要重做系统，还会造成数据丢失，所有可以使用备份和恢复技术。

**`Linux` 的备份和恢复很简单，有两种方式：**
1. 把需要的文件（或者分区）用 `TAR` 打包就行，下载需要恢复的时候，在解压覆盖即可
2. 使用 `dump` 和 `restore` 命令

### 安装 `dump` 和 `restore`

如果 Linux 系统上没有 dump 和 restore 指令，需要先安装

```bash
yum -y install dump
yum -y install restore
```

![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221115112834.png)

### 使用 `dump` 完成备份

**基本介绍**
- `dump` 支持分卷和增量备份（所谓的增量备份是指备份上次备份后 修改/增加过的文件，也称为差异备份）

**`dump` 语法说明**

```bash
dump [-cu] [-123456789] [-f <备份后文件名>] [-T <日期>] [目录或文件系统]
dump []-wW
```

- `-c`：创建新的归档文件，并将由一个或者多个文件参数所指定的内容写入归档文件的开头
- `-123456789`：备份的层级，0是最完整备份会备份所有文件，指定0以上层级，则备份至上一次备份依赖修改或者新增的文件，到9后，可以再次轮替
- `-f <备份后文件名>`：指定备份后文件名
- `-j`：调用 `bzlib` 库压缩备份文件，也就是将备份后的文件压缩成 `bz2` 格式，让文件更小
- `-T <日期>`：指定开始备份的时间和日期
- `-u`：备份完毕后，在 `/etc/dumpdares` 中记录备份的文件系统，层级、日期与时间等
- `-t`：指定文件名，若该文件已存在备份文件中，则列出名称
- `-W`：显示需要备份的文件及其最后一次备份的层级、时间、日期
- `-w`：与 `-W` 类似，但仅显示需要备份的文件

**示例**
1. 将 `/boot` 分区所有内容被分到 `/opt/boot.bak.bz2` 文件中，备份层级为 0
```bash
dump -0uj -f /opt/boot.bak0.bz2 /boot
```
![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221115115255.png)

2. 在 `/boot` 分区下拷贝一个文件，备份层级为 1 （只备份上次使用层级 0 备份后发生改变的数据）
```bash
dump -1uj -f /opt/boot.bak1.bz2 /boot
```
![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221115115426.png)

> 通过 `dump` 命令可以在无人值守的时候配合 `crontab` 进行备份

`dump -W` ：显示需要备份的文件及其最后一次备份的层级、时间、日期
![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221115115557.png)

查看备份时间文件：`cat /etc/dumpdates`

![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221115115625.png)

**`dump` 备份文件或者目录**

之前我们备份分区时，时可以支持增量备份的，如果备份文件或者目录，不在支持增量备份，即只能使用 0 级别的备份
```bash
# 使用dump备份 /etc 整个目录
dump -0j -f /opt/etc.bak.bz2 /etc/

# 下面这条语句会报错： DUMP: Only level 0 dumps are allowed on a subdirectory
#                    DUMP: The ENTIRE dump is aborted.
dump -1j -f /opt/etc.bak.bz2 /etc/
```

>如果是重要的备份文件，比如数据区，建议将文件上传到其它服务器拔除，不要将鸡蛋放在同一个篮子

### 使用 `restore` 完成恢复

**基本介绍**
- `restore` 命令用来恢复已备份的文件，可以从 `dump` 生成的备份文件中恢复原文件

**`restore` 基本语法**
- `restore [模式选项] [选项]`

下面四个模式不能混用，一次命令中，只能使用一种
- `-C`：使用对比模式，将备份的文件与已存在的文件相互对比
- `-i`：使用交互模式，在进行还原操作时，`restore` 指令将依序询问用户
- `-r`：进行还原模式
- `-t`：查看模式，看备份文件有哪些文件

选项
- `-f <备份文件>`：从指定的文件中读取备份数据，进行还原操作

**示例**

1. `restore` 目录比较模式，比较备份文件和还原模式的区别

```bash
mv /boot/hello.java /boot/hello100.java
restore -C -f boot.bak1.bz2 // 注意和最新的文件比较
```
![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221115121429.png)

```bash
mv /boot/hello100.java /boot/hello.java
restore -C -f boot.bak1.bz2
```
![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221115121453.png)

2. `restore` 命令查看模式，看备份文件有哪些数据和文件

```bash
restore -t -f boot.bak0.bz2
```
![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221115121837.png)

3. `restore` 命令还原模式，注意：如果你有增量备份，需要把增量备份文件也进行恢复，有几个增量备份文件，就需要恢复几个，按顺序来恢复即可。
```bash
mkdir /opt/boottmp
cd /opt/boottmp
restore -r -f /opt/boot.bak0.bz2 # 恢复到第一次完全备份的状态
restore -r -f /opt/boot.bak1.bz2 # 恢复到第二次增量备份的状态
```

![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221115122134.png)

4. `restore` 命令恢复备份的文件，或者整个目录的文件
```bash 
# 基本语法：restore -r -f 备份好的文件
mkdir etctmp
cd etctmp/
restore -r -f /opt/etc.bak0.bz2
```
![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221115122422.png)
