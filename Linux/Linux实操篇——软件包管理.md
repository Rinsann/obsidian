### `rpm` 包管理
**介绍**
`rpm` 用于互联网下载包的打包及安装工具，它包含在某些`Linux`分发版中。
它生成具有 `.RPM` 扩展名的文件，`RPM` 是 `RedHat Package Manager`（`RedHat` 软件包管理工具）的缩写，类似 `windows` 的 `.exe`，这一文件格式名称虽然都打上了 `RedHat` 的标识，但理念是通用的。

`Linux` 的分发版本都有采用（`suse，redhat，centos` 等），算是公认的行业标准。

**`rpm` 包的简单查询指令**
- 查询已安装的 `rpm` 列表：`rpm -qa | grep xxx` 
![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221112152424.png)

**`rpm` 包名基本格式**
- 一个 `rpm` 包名：`firefox-60.2.2-1.el7.centos.x86_64`
- 名称：`firefox`
- 版本号：`60.2.2-1`
- 适用操作系统：`el7.centos.x86_64`，表示 c`entos.7x` 的64位系统
- 如果是 i686、i386表示32位系统，`noarch` 表示通用

**rpm 包的其他查询指令**
- `rpm -qa`：查询所有的 `rpm` 软件包
- `rpm -qa | more` 
- `rpm -qa | grep X [rpm -qa | grep firefox]`
- 查询软件包是否安装：`rpm -qa firefox`
- 查询软件包信息：`rpm -qi firefox`![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221112152934.png)
- 查询软件包中的文件：`rpm -ql firefox`
- rpm -qf 文件全路径 查询文件所属的软件包
-  `rpm -qf /etc/passwd`
-  `rpm -qf /root/install.log`

**卸载 `rpm` 包**
- 基本语法：rpm -e RPM包的名称

**细节**
1. 如果其他软件包依赖于要卸载的软件包，卸载时则会报错
2. 比如是要删除 `foo` 这个 `rpm` 包，可以增加参数 `--nodeps`，就也可以强制删除，但是一般不推荐，因为依赖于该软件包的程序可能无法运行
3. `rpm -e --nodeps foo`

**安装 rpm 包**
- 基本语法：rpm -ivh RPM包全路径名称
- 参数
	- `i=install` 安装
	- `v=verbose` 提示
	- `h=hash` 进度条
![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221112154103.png)



### `yum` 包管理
**介绍**
- `Yum` 是一个 `Shell` 前端软件包管理器，基于 RP`M` 包管理，能够从指定的服务器自动下载 RPM `包并且安装`，可以自动处理依赖性关系，并且一次安装所有依赖的软件包

**`yum` 的基本指令**
- `yum list | grep xxx`：查询 `yum` 服务器是否有需要的软件
- `yum install xxx`：安装指定的 `yum` 包

**示例**
- `rpm -e firefox`
- `yum list | grep firefox`
- `yum install firefox`

#### yum源是什么
`linux` 下方便安装软件的优秀工具称之为 `yum` 工具，`linux` 的二级制软件包一般为 `rpm` 包，类似于 `windows` 下的 `exe` 程序。通过 `yum` 工具安装，默认获取的 `rpm` 包的软件配置一般为国外 `centos` 官方源下载，所以安装软件会速度较慢，因此需要将默认 `rpm` 包的配置由国外官方源改为国内

**如何更换yum源？**

1. 首先进入`linux`的 `etc/yum.repos.d` 目录下，将`Centos-Base.repo`进行备份
```bash
cd /etc/yum.repos.d
zip Centos-Base.repo.zip Centos-Base.repo

```
2. 删除`Centos-Base.repo`
```bash
rm Centos-Base.repo
```
3. 下载`yum`源到`etc/yum.repos.d`文件目录下
```bash
wget -O /etc/yum.repos.d/CentOS-Base.repo http://mirrors.aliyun.com/repo/Centos-6.repo
```
4. 清理yum并生成缓存
```bash
yum clean all
```

这里替换的是阿里提供的 `yum` 源，我们也可以将自己的 `iso` 镜像或者光盘配置为 `yum` 源
```bash
阿里：wget -O /etc/yum.repos.d/CentOS-Base.repo http://mirrors.aliyun.com/repo/Centos-6.repo
网易：wget -O /etc/yum.repos.d/CentOS-Base.repo http://mirrors.163.com/.help/CentOS7-Base-163.repo
```
