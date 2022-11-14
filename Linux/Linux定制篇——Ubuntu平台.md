### `Ubuntu` 介绍
`Ubuntu` （乌班图）是一个以桌面应用为主的开源 `GNU/Linux` 操作系统，`Ubuntu` 是基于 `GNU/Linux`，支持 `x86`、`amd64`（即`x64`）和 `ppc` 架构，由全球化的专业开发团队（`Canonical Ltd`）打造。

专业的 `Python` 开发者一般会选择 `Ubuntu` 这款 `Linux` 系统作为生产平台。
`Ubuntu` 和 `CentOS` 都是基于 `GNU/Linux` 内核的，因此基本使用和 `CentOS` 几乎一样，它们的各种指令大部分都可以通用，只有界面和预安装的软件有所差别
下载地址：`https://releases.ubuntu.com/20.04/`

### 安装的步骤
1. 开启 `bios` 虚拟化支持
2. 新建虚拟机
3. 选择镜像文件
4. 设置用户名密码
5. 设置虚拟机名称
6. 设置磁盘大小
7. 自定义硬件，内存`2G`、处理器`4`，网络设置 `NAT` 模式
8. 点击完成
9. 然后等待一段时间就好了，`Ubuntu` 会自动设置
10. 进入后跳过所有的向导，然后打开 `firefox` 看看能不能上网就行了


![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221114140907.png)
![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221114140851.png)
![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221114140933.png)
![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221114141002.png)
![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221114141100.png)
![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221114141110.png)
![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221114141124.png)
![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221114141221.png)
![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221114141239.png)
![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221114141733.png)
![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221114142828.png)


### 设置 `Ubuntu` 支持中文

默认安装的 Ubuntu 中只有英文，因此不能显示汉字，要正确的显示汉字，需要安装中文语言包

**安装中文支持的步骤：**
1. 单击左侧图标栏打开 Language Support 菜单，点击打开 Language Support（语言支持）选修课。
2. 点击 Install / Remove Languages，在弹出的选项卡中下拉找到 Chinese(Simplified)，中文简体，在后面的选项框中打勾，然后点击 Apply Changes 提交，系统会自动联网下载中文语言包。
3. 这时 "汉语（中国）"在最后一位，因为当前第一位的是 "English"，所以默认显示的都是英文，将"汉语（中国）"设置到第一位，直接拖动即可。
4. 设置好不会即可生效，需要重启。
![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221114142509.png)
![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221114143022.png)
![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221114143029.png)
![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221114143140.png)

### `Ubuntu` 的 `root` 用户

**介绍**
安装 `Ubuntu` 成功后，都是普通用户权限，并没有最高 `root` 权限，如果需要使用 `root` 权限的时候，通常都是在命令前加上 `sudo`。

也可以使用 `su` 命令直接切换到 `root` 用户，但是如果没有给 `root` 设置初始密码，就会抛出一个错误 `su: Authentication failure`。

**给 `root` 设置密码并使用**
1. 输入 `sudo password` 命令，输入一般用户密码并设置 `root` 用户密码。
2. 设定 `root` 密码成功后，输入 `su` 命令，并输入刚刚设置的 `root` 密码，就可以切换 `root` 用户了，提示符 `$` 代表一般用户，提示符 `#` 代表 `root` 用户。
3. 输入 `exit` 命令，退出 `root` 用户并返回到一般用户
![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221114143922.png)

### `Ubuntu` 下开发 `Python`

说明：安装好 `Ubuntu` 后，默认就已经安装好了 `Python` 的开发环境
![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221114144031.png)
![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221114144325.png)
