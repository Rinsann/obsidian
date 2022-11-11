### `Linux` 分区
**原理介绍**
1. `Linux` 系统无论有几个分区，分给哪一个目录使用，它归根结底就只有一个根目录，一个独立且唯一的文件结构，`Linux` 中每个分区都是用来组成整个文件系统的一部分。
2. `Linux` 采用了一种叫做 "载入"的处理方法，它的整个文件系统中包含了一整套的文件和目录，且将一个分区和一个目录联系起来，这时要载入的一个分区将使它的存储空间在一个目录下获得。
![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221111135353.png)


**查看所有设备挂载情况**
命令：`lsblk` 或者 `lsblk -f`
![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221111134313.png)

**硬盘说明**
1. `Linux` 硬盘分`IDE`硬盘和`SCSI`硬盘，目前基本是 `SCSI` 硬盘
2. 对于 `IDE` 硬盘，驱动器标识符为 `"hdx~"`，其中 `"hd"` 表明分区所在设备的类型，这里是指 `IDE` 硬盘了 ，`"x"` 为盘号（`a` 为基本盘，`b` 为基本从属盘，`c` 为辅助主盘，`d` 为辅助从属盘），`"~"` 代表分区，前四个分区用数字1到4表述，它们是主分区或者扩展分区，从5开始就是逻辑分区。例如：`hda3` 表示为第一个 `IDE` 硬盘上的第三个主分区或者扩展分区，`hdb2` 表示为第二个 `IDE` 硬盘上的第二个主分区或扩展分区。
3. 对于 `SCSI` 硬盘则标识为 `"sdx~"`，`SCSI` 硬盘使用 `"sd"` 来标识分区所在设备的类型，其余则和 `IDE` 硬盘标识方式一致。

### 挂载
**如何增加一块硬盘**
1. 虚拟机添加硬盘
2. 分区
3. 格式化
4. 挂载
5. 设置可以自动挂载

**虚拟机增加硬盘步骤1**
在 **虚拟机** 菜单中，选择设置，然后设备列表里添加硬盘，然后一直下一步，中间只需要选择磁盘大小就可以了。然后**重启系统**，重启才能识别到。
![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221111140107.png)
**虚拟机增加硬盘步骤2**
分区命令 `fdisk /dev/sdb`
开始对 `/sdb` 分区
- `m` 显示命令列表
- `p` 显示磁盘分区 同 `fdisk -l`
- `n` 新增分区
- `d` 删除分区
- `w` 写入并退出
> 开始分区后输入`n`，新增分区，然后选择`p`，分区类型为主分区。两次回车默认剩余全部空间，最后输入`w`写入分区并退出，若不保存退出输入`q`

![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221111142414.png)
![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221111142701.png)
**虚拟机增加硬盘步骤3**
格式化磁盘
分区命令：`mkfs -t ext4 /dev/sdb1`
其中 `ext4` 是分区类型
![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221111144126.png)

**虚拟机增加硬盘步骤4**
挂载：将一个分区与一个目录联系起来
mount 设备名称 挂载目录，例如：`mount /dev/sdb1 /newdisk`
卸载：umount 设备名称 或者 挂载目录
`umount /dev/sdb1` 或者 `umount /newdisk`
![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221111144444.png)

> 注意：用命令行挂载重启后会失效

**虚拟机增加硬盘步骤5**
永久挂载：通过修改 `/etc/fstab` 实现
添加完成后执行 `mount -a` 即可生效
重启后依然是挂载状态
![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221111150540.png)

**/etc/fstab 文件参数解释**
![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221111145601.png)
第五列是 `dump` 备份设置。

当其值设置为1时，将允许 `dump` 备份程序备份；设置为0时，忽略备份操作；

第六列是 `fsck` 磁盘检查设置。
其值是一个顺序。当其值为0时，永远不检查；而 / 根目录分区永远都为1。其它分区从2开始，数字越小越先检查，如果两个分区的数字相同，则同时检查。

### 磁盘情况查询
**查询系统整体磁盘情况**

基本语法
	- `df -h`![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221111150653.png)
查询指定目录的磁盘占用情况，默认为当前目录
基本语法：`du -h`
	- `-s`：指定目录占用大小汇总
	- `-h`：带计量单位
	- `-a`：含文件
	- `--max-depth=1`：子目录深度
	- `-c`：列出明细的同时，增加汇总值![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221111151428.png)

### 磁盘情况-实用指令

1. 统计 `/opt` 文件夹下的文件个数
	- `ls -l /opt | grep "^-" | wc -l`![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221111151832.png)
2.  统计 `/opt` 文件夹下的目录个数
	- `ls -l /opt | grep "^d" | wc -l`
3.  统计 `/opt` 文件夹下文件的个数，包括子文件夹里的
	- `ls -lR /opt | grep "^-" | wc -l`
4.  统计 `/opt` 文件夹下目录的个数，包括子目录里的
	- `ls -lR /opt | grep "^d" | wc -l`
5. 以树状显示目录结构
	- `tree /opt`，默认情况没有安装 `tree`，可以输入`yum install tree`安装。![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221111152232.png)
