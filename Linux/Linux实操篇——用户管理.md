### 基本介绍
Linux 系统是一个多用户多任务的操作系统，任何一个要使用系统资源的用户，都必须首先向系统管理员申请一个账号，任何以这个账号的身份进入系统
### 添加用户
**基本语法**
```bash
useradd 用户名
```
**细节说明**
1. 当创建用户成功后，会自动的创建和用户名同名的家目录（默认家目录在 `/home/用户名`）
2. 也可以通过 `useradd -d 指定目录 新的用户名`，给新创建的用户指定家目录
![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221107144835.png)

### 指定/修改密码
**基本语法**
```bash
passwd 用户名
```

![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221107145117.png)

### 删除用户
**基本语法**
```bash
userdel 用户名
```

**可选**
1. 删除用户 `milan`，但是保留家目录 `userdel milan`![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221107145556.png)![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221107145644.png)

2. 删除用户以及用户主目录，比如：`userdel -r test`

**细节说明**
一般情况下，我们建议保留家目录的。

### 查询用户信息指令
**基本语法**
```bash
id 用户名
```

![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221107150145.png)


>当用户不存在时，返回无此用户

### 切换用户

**介绍**
在操作 `Linux` 系统的时候，如果当前用户的权限不够，可以通过 `su -` 指令，切换到高权限用户，比如 `root`
**基本语法**
```bash
su - root
```

1. 从权限高的用户切换到权限低的用户，不需要输入密码，反之需要
2. 当需要返回原来的用户时，使用 `exit/logout` 指令

### 查看当前用户/登录用户

**基本语法**
```bash
whoami/who am I
```
![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221107150728.png)
`whoami` 查看的是当前登录用户信息，`who am i` 查看的是第一次连接和登录的用户信息

### 用户组

**介绍**
类似于角色，系统可以对有共性（权限）的多个用户进行统一的管理

**新增组**
指令：`groupadd 组名`

**删除组**
指令（基本语法）：`groupdel 组名`

**增加用户时直接加上组**
指令（基本语法）：`useradd -g 用户组 用户名`
![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221107151556.png)

**修改用户的组**
指令（基本语法）：`usermod -g 用户组 用户名`
![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221107151736.png)

### 用户和组相关文件

**`etc/password` 文件**
用户（user）的配置文件，记录用户的各种信息
每行的含义：用户名:口令:用户标识符:组标记号:注释性描述:主目录:登录`Shell`
![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221107152625.png)

**`etc/shadow` 文件**
口令的配置文件
每行的含义：登录名:加密口令:最后一次修改时间:最小时间间隔:最大时间间隔:警告时间:不活动时间:失效时间:标志
![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221107152703.png)

**`etc/group` 文件**
组（`group`）的配置文件，记录 `Linux` 包含的组的信息
每行的含义：组名:口令:组标识符:组内用户列表（隐藏）
![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221107152734.png)