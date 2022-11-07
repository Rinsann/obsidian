
### 虚拟机克隆

如果你已经安装了一台`Linux`操作系统，还需要更多的时候（比如需要模拟集群），没有必要重新安装，你只需要克隆就可以。

- 方式一：直接拷贝一份安装好的虚拟机文件，比如：我直接找到之前安装在`D`盘的`RinCentOS`文件夹，`ctrl+c` 复制一份就可以了，然后使用 `vmware` 打开这样就多出来一份新的 `Linux` 系统了![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221106100942.png)![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221106101255.png)![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221106101337.png)选择打开这个`.vmx`的文件即可。
- 方式二：使用`vmware`的克隆操作，右键`Linux`系统-->管理-->克隆![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221106101625.png)![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221106101651.png)![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221106101717.png)第一个克隆之前系统的引用，这样打开的还是同一个系统，第二个创建完整克隆，本质其实也是一种拷贝，一般都选第二个。![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221106101945.png)![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221106102016.png)![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221106102137.png)这样我们就创建了一个完全一样的`Linux`系统了，用户名和密码安装的软件都是一模一样的。

>注意：克隆时，需要先关闭 `Linux` 系统


### 虚拟机快照

如果你在使用虚拟机系统的时候（比如 `Linux`），你想要回到原先的某一个状态，也就是说担心可能有些误操作造成系统异常，需要回到原先某个正常的状态，`vmware` 提供了一个快照管理的功能。

![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221106102843.png)

首先进入到之前创建的 Linux 系统，然后右键选择快照-->拍摄快照
![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221106103224.png)
![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221106103243.png)
当我们创建了快照之后可以在快照管理器中查看。
![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221106103439.png)

怎么回退到初始状态呢？首先点击第一个快照，然后选择转到
![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221106103616.png)
重启后就回到了初始状态了，桌面一个文件夹都没有。
![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221106103649.png)
再重新转到快照 B，如果在B继续拍摄快照D，那么节点就是从B开始的

![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221106103729.png)
![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221106103904.png)

### 虚拟机的迁移和删除

虚拟机系统安装好了，它的本质就是文件（放在文件夹中），因此虚拟机系统的迁移很方便，可以把安装好的虚拟系统这个文件夹整体**拷贝或者剪切**到另外的位置使用。删除也很简单，`用vmware` 进行移除，在点击菜单 --> 从磁盘删除即可，或者直接手动删除虚拟机系统对应的文件夹。

![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221106104610.png)
移除后还需要把磁盘里的文件删除，也可以选择管理-->从磁盘删除![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221106104757.png)


### 安装 `vmtools`

**介绍**
1. `vmtools` 安装后，可以让我们在 `windows` 下更好的管理 `vm` 虚拟机
2. 可以设置 `windows` 和 `centos` 的共享文件夹

**安装 `vmtools` 的步骤**

1. 进入 `centos`
2. 点击 `vm` 菜单 --> `install vmware tools`
3. `centos` 会出现一个 `vm` 的安装包，`xxx.tar.gz`
4. 拷贝到 `/opt`
5. 使用解压命令 `tar`，得到一个安装文件
6. 进入该 `vm` 解压的命令，`/opt` 目录下
7. 安装 `./vmware-install.pl`
8. 全部使用默认设置即可，就可以安装成功
9. 注意：安装 `vmtools` 需要有 `gcc`

进入 `CentOS` 系统`root`用户， 选择弹出![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221106105852.png)
关机，设置中修改成自动检测，重新开机 ![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221106110024.png)
然后再开机过程中选择虚拟机-->重新安装，开机后可能是灰色的不可选。
![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221106110416.png)

看见这个光盘-->点击进入
![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221106110648.png)
然后将这个`tar.gz`文件夹拷贝到 `/opt` 目录下![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221106110748.png)
右键复制-->打开主文件夹-->其他位置-->计算机-->opt-->粘贴![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221106111000.png)
桌面右键-->打开终端，输入命令
```bash
cd /opt/
tar -zxvf VMwareTools-10.3.23-165xxxxxx.tar.gz
cd vmware-tools-distrib //进入到解压后的目录
./vmware-install.pl //安装，一直回车即可，不过在最后一个提问需要输入 no 
```

![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221106111804.png)

设置共享文件夹，windows主机中新建myshare文件夹，然后虚拟机设置中选项-->共享文件夹-->设置主机路径-->下一步-->完成
![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221106112658.png)

虚拟机系统中的共享文件夹位置：主文件夹-->其他位置-->计算机-->`mnt`-->`hgfs`-->`myshare`![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221106112958.png)
