### `VM` 和 `Linux` 的安装

**安装 `vm` 和 `Centos`**

- 基本说明：学习 `Linux` 需要一个环境，我们需要创建一个虚拟机，`然后再虚拟机上安装一个CentOS` 系统来学习

1. 先安装 `virtual machine 15.5`
2. 再安装 `Linux`（CentOS 7.6/CentOS 8.1）
3. 原理示意图
	- ![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221105114247.png)

### 安装 VM 和 CentOS

- vmware15.5下载
	- 官方地址：https://www.vmware.com/products/workstation-pro/workstation-pro-evaluation.html
	- 其他地址：https://www.nocmd/windows/740.html

**vm安装步骤**

> 需要先在BIOS开启**虚拟化设备**支持(f2/f10)
![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221105120246.png)
![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221105120253.png)
![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221105120310.png)
> 修改安装位置，不建议安装在`C`盘
![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221105120406.png)

![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221105120414.png)
![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221105120422.png)
![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221105120504.png)
跳过，选择试用30天即可
![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221105120556.png)


**CentOS 7.6安装**

- Centos 下载地址
	1. http://mirrors.163.com/centos/7.9.2009/isos/x86_64/CentOS-7-x86_64-DVD-2009.iso
	2. https://mirrors.aliyun.com/centos/
	3. ![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221105121319.png)
	4. 进入vmware软件
	5. 点击创建新的虚拟机![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221105121517.png)
	6. 选择稍后安装操作系统![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221105121603.png)
	7. 一定要选择Red Hat Linux7这个版本 ![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221105121650.png)
	8. 尽量将新建安装到空间较大的盘符（c盘除外）![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221105121832.png)
	9. 选择`CentOS`虚拟机最大的空间（不是马上占用这么多），选择拆分成多个文件（默认就行） ![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221105121919.png)
	10. 选择自定义硬件![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221105122045.png)
	11. 内存，使用推荐的 2个G 就行 ![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221105122109.png)
	12. 处理器（取决于主机）![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221105122352.png)
	13. 光驱，先跳过![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221105122426.png)

	14. 网络适配器，三种主要模式使用默认的，暂且跳过。![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221105122437.png)
	15. 其他的都默认就行。
	16. 然后就是设置ISO，选择你现在的ISO文件路径即可 ![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221105122602.png)![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221105122652.png)
	17. 点击确定。
	18. 点击开启虚拟机 ![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221105122753.png)
	19. 











