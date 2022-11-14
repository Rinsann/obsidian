
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