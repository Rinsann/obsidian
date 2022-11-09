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
