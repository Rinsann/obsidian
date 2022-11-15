
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
2. 




