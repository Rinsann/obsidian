
## 基本介绍
通过裁剪现有的 `Linux` 系统（`CentOS7.6`）来创建一个属于自己的 `mini Linux` 小系统，可以加深我们对 `Linux` 系统的理解

## 基本原理

启动流程介绍，制作 `Linux mini`版之前。再了解一些 `Linux` 启动的流程：
1. 首先 `Linux` 要通过自检，检查硬件设备有没有故障
2. 如果有多块启动盘，需要在 `BIOS` 中选择启动磁盘
3. 启动 `MBR` 中的 `bootloader` 引导程序
4. 加载内核文件
5. 执行所有进程的父进程，`systemd`
6. 欢迎界面

在 `Linux` 的启动流程中，加载内核文件时关键文件：
- `kernel` 文件：`vmlinuz-3.10.0-957.el7.x86_64`
- `initrd` 文件：`initramfs-3.10.0-957,.el7.x86_64.img`

## 制作`mini Linux` 思路分析
![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221114205722.png)

1. 在现有的 `Linux` 系统上加上一块硬盘 `/dev/sdb`，在硬盘上分两个区，一个是 `/boot`，一个是 `/`，并将其格式化。需要明确的是，现在加的这个硬盘在现有 `Linux` 系统中是 `/dev/sdb`，但是，当我们把东西全部设置好时，要把这个硬盘拔除，放在新系统上，此时，就是 `/dev/sda`
2. 在 `/dev/sdb` 硬盘上，将其打造成独立的 `Linux` 系统，里面的所有文件是需要拷贝进去的
3. 作为能独立运行的 `Linux` 系统，内核是一定不能少，要把内核文件 `initramfs` 文件也一起拷贝到 `/dev/sdb` 上
4. 以上步骤完成，自制的 `Linux` 就完成了，创建一个新的 `Linux` 虚拟机，将其硬盘指向我们创建的硬盘，启动即可。
![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221114210143.png)

## 操作步骤

1. 首先，我们在现有的 `Linux` 中添加一块大小为 20G 的硬盘![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221114210430.png)![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221114210517.png)![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221114210530.png)![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221114210549.png)![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221114210611.png)![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221114210700.png)
2. 添加完成后重启，可以是 `lsblk` 查看，然后通过 `fdisk` 来给我们的 `/dev/sdb` 进行分区![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221115090654.png)![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221115090724.png)
3. 接下来 ，对 `/dev/sdb` （我之前分过区所以图片显示`sdc`）的分区进行格式化
	- 输入`mkfs.ext4 /dev/sdc1`和`mkfs.ext4 /dev/sdc2` ![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221115091049.png)
4. 创建目录，并挂载新的磁盘
```bash
mkdir -p /mnt/boot /mnt/sysroot
mount /dev/sdc1 /mnt/boot
mount /dev/sdc2 /mnt/sysroot
```

5. 安装 `grub`，将内核文件拷贝至目录磁盘
```bash
grub2-install --root-directory=/mnt /dev/sdc
# 看看是否安装成功
hexdump -C -n 512 /dev/sdc
rm -rf /mnt/boot/*  # 先清除，不然需要重复的去确认覆盖文件
cp -rf /boot/* /mnt/boot/
```
![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221115092017.png)

6. 修改 `grub2/grub.cfg` 文件，标红的部分需要使用指令来查看。
![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221115094532.png)

![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221115092106.png)在 `grub.cfg` 文件中，红色部分用上面的 `sdc1` 的 `UUID` 替换，蓝色部分用 `sdc2` 的 `UUID` 替换，紫色部分是添加的，`selinux=0 init=/bin/bash` 表示 `selinux` 关掉，同时设置一下 `init`，告诉内核不用再去找这个程序了，不然开机的时候会出现错误。
![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221115093234.png)
![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221115093641.png)

同时下面一样的修改这几处地方
![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221115094157.png)

7. 创建目标主机根文件系统
```bash
mkdir -pv /mnt/sysroot/{etc/rc.d,usr,var,proc,sys,dev,lib,lib64,bin,sbin,boot,srv,mnt,media,home,root}
```
![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221115094742.png)

8. 拷贝需要的 bash（也可以拷贝你需要的指令）和库文件给新的系统使用
```bash
cp /lib64/*.* /mnt/sysroot/lib64/
cp /bin/bash /mnt/sysroot/bin/
```
![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221115094849.png)
![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221115094926.png)

9. 我们现在就可以创建一个新的虚拟机，然后将默认分配的硬盘移除掉，指向我们刚刚创建的磁盘即可。![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221115095108.png)
![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221115095135.png)
![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221115095246.png)
![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221115095350.png)
![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221115095414.png)
![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221115095847.png)
这里我的名字不知道为什么改变了，不过成功了
![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221115095627.png)
![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221115095943.png)

10. 其实这个时候很多指令都不能使用了，比如 `ls`、`reboot` 等，可以将需要的指令拷贝到对应的目录即可

11. 如果需要拷贝指令，重新进入原来的 `Linux` 系统拷贝相应的指令，比如将 `/bin/ls` 拷贝到 `/mnt/sysroot/bin` 将 `/sbin/reboot` 拷贝到 `/mnt/sysroot`
```bash
mount /dev/sdc2 /mnt/sysroot/ # 重启后挂载会失效所以需要重新挂载
cp /bin/ls /mnt/sysroot/bin
cp /bin/systemctl /mnt/sysroot/bin/
co /sbin/reboot /mnt/sysroot/bin/
```
![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221115100651.png)

12. 再次重启新的 `Linux` 系统，就可以使用 `ls` 和 `reboot` 命令了
![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221115100813.png)
