### 为什么需要远程登录Linux

1. Linux 服务器很多时候是公司小组共享
2. 正式上线的项目运行在公网
3. 因此程序员需要远程登录到Linux进行项目管理或者开发
4. 远程登录客户端有 `Xshell`，`Xfpt`，`MobaXterm` https://mobaxterm.mobatek.net/download.html 这些工具都大同小异，使用那个都行

Linux 查看IP地址
```bash
ifconfig 
或
ip addr
```

那个都可以，找到 `ens33` 下的 `inet` 地址就行，然后再 `cmd` 中 通过 `ping` 命令检查是否能够 `ping` 通
![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221107121232.png)
![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221107121415.png)
这样就是可以 `ping` 通了，然后使用 `MobaXterm` 或者 其他的工具连接就行了。
`MobaXterm` 是这样用的，下载好后点击 `session` --> `ssh` 连接-->
![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221107121536.png)
输入刚刚查到的`IP`地址![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221107121640.png)
勾选 `Specify username`，点旁边的小人打开新窗口点`new`
![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221107121757.png)
![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221107121928.png)

`MobaXterm`上传文件很简单，只需要直接把 `windows` 主机上的文件拉到 `MobaXterm` 左侧的位置就能直接上传了
![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221107122828.png)
把左侧边栏下面的这个勾上，就能在你输入命令的时候同步当前目录显示了，比如 `cd /opt/`，左边就会显示 `/opt`目录了，然后只需要把上传的文件拉到这边来=上传，直接把里面的文件拉到`windows` 主机=下载。OK，非常简单！
![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221107123150.png)
