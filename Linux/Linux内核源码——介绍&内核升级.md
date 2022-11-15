## 为什么要阅读 `Linux` 内核

- 爱好，就是喜欢 `Linux`（黑客精神）
- 想要深入理解 `Linux` 底层运行机制，对操作系统有深入了解

阅读 `Linux` 内核，会对整个计算机体系有一个更深刻的认识，作为开发者，不管是从事驱动开发，应用开发还是后台开发，都需要了解操作系统内核的运行机制，这样才能写出更好的代码。

作为开发者不应该只是局限在自己的领域，设计的模块看起来小，但是不了解进程的调用机制，不知道进程为什么会阻塞、就绪、执行几个状态，那么很难写出优质的代码。

作为有追求的程序员，还是应该深入了解一个操作系统的底层机制，（比如 `Unix/Linux`）最后是深入源码级别，这样写多线程高并发程序，包括架构，优化，算法等。深度是不一样的，不求把整个庞大的 `Linux` 内核每一行都读懂，至少能看懂几个核心的模块。

## `Linux0.01` 内核源码
**基本介绍**
`Linux` 的内核源码可以直接从网上下载，解压缩后文件一般也都在 `Linux` 目录下，内核源码有很多版本，可以先从 0.01 版入手，总共代码量 1W 行左右，最新版本 6 总代码超过了 `700W` 行，非常庞大。

> 内核地址：`https://www.kernel.org/`
![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221115102059.png)

很多人害怕阅读源码，特别是像 `Linux` 内核这样大而且复杂的系统代码，阅读起来非常困难，但是也不是想象的那么高不可攀，建议可以先从 `Linux0.01` 版本入手。

### Linux 0.01 内核源码目录&阅读

**阅读内核源码技巧**
1. `Linux 0.01` 的阅读需要懂 `C` 语言
2. 阅读源码之前，应该指定 `Linux` 内核源码的整体分布情况，现代操作系统一般由进程管理、内存管理、文件系统、驱动程序、和网络等组成，`Linux` 内核源码的各个目录大致与此对应。
3. 在阅读顺序上，有纵向与横向之分，所谓纵向就是顺着程序的执行顺序逐步进行；所谓横向就是按模块进行，它们经常结合在一起进行。
4. 对于 `Linux` 启动的代码可以顺着 `Linux` 的启动顺序一步步来阅读；对于像内存管理部分，可以单独拿出来进行分析，实际上这是一个反复的进程，不可能读一遍就理解。

**`Linux` 内核源码阅读&目录介绍& `main.c` 说明**

![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221115105542.png)

`main.c` 说明
![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221115110158.png)


### `Linux` 内核最新版和内核升级

下载 & 解压最新版
```bash
wget https://cdn.kernel.org/pub/linux/kernel/v5.x/linux-5.8.16.tar.gz
```

**`linux` 内核升级示例**
将centos系统从7.6 内核升级到 7.8版本内核（兼容性问题）
![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221115110903.png)

```bash
uname -a # 查看当前内核版本
yum info kernel -q # 检测内核版本，显示可升级的内核版本
yum update kernel # 升级内核
yum list kernel -q # 查看已安装的内核
```

![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221115111524.png)
![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221115111759.png)
![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221115111956.png)
![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221115112038.png)
