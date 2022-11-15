### 搭建JavaEE环境
**安装步骤**
1. `mkdir /opt/jdk`
2. 通过 `MobaXterm` 上传到 `/opt/jdk` 下
3. `cd /opt/jdk`
4. 解压 `tar -zxvf jdk-8u261-linux-x64.tar.gz`![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221112162155.png)
5. `mkdir /usr/local/java`
6. `mv /opt/jdk/jdk.1.8.0_261 /usr/local/java`![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221112162357.png)
7. 配置环境变量的配置文件 `vim /etc/profile`
8. `export JAVA_HOME=/usr/local/java/jdk1.8.0_202`
9. `export PATH=$JAVA_HOME/bin:$PATH`
10. `source /etc/profile` 让文件（环境变量）生效![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221112163031.png)
**测试**
编写一个 `Hello.java` 输出 `"Hello World!"`
![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221112163246.png)

### tomcat 安装
**步骤**
1. 上传安装文件，并解压到 `/opt/tomcat`
2. 进入解压目录 `/bin`，启动 tomcat `./startup.sh`![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221112163859.png)
3. 开放端口 `8080`![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221112164130.png)
**测试安装是否成功**
![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221112164212.png)
![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221112164405.png)

### 安装 idea 
**步骤**
1. 下载地址：`https://www.jetbrains.com/idea/download/#section=linux`
2. 解压缩到 `/opt/idea`
3. 启动 `idea`， `bin` 目录下运行 `./idea.sh`，配置 `jdk`
4. 编写 Hello World 程序

### mysql5.7 安装
**步骤**
1. 新建文件夹 `/opt/mysql` ,并 `cd` 进入
2. 运行 `wget http://dev.mysql.com/get/mysql-5.7.26-1.el7.x86_64.rpm-bundle.tar`，下载 `mysql` 安装包
3. 运行 `tar -xvf mysql-5.7.26-1.el7.x86_64.rpm-bundle.tar`![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221112185844.png)
4. 运行 `rpm -qa | grep mari`，查询 `mariadb` 相关安装包，因为 `contos7.6` 自带了类似 `mysql` 数据库的 `mariadb` ，会和 `mysql` 冲突要先删除
5. 运行 `rpm -e --nodeps mariadb-libs` 和 `rpm -e --nodeps marisa`，卸载。
6. 然后开始安装 `mysql`，依次运行如下命令：
```bash
rpm -ivh mysql-community-common-5.7.26-1.el7.x86_64.rpm
rpm -ivh mysql-community-libs-5.7.26-1.el7.x86_64.rpm
rpm -ivh mysql-community-client-5.7.26-1.el7.x86_64.rpm
rpm -ivh mysql-community-server-5.7.26-1.el7.x86_64.rpm
```
7. 运行 `systemctl start mysqld.service`，启动 `mysql`
8. 然后开始设置 `root` 用户密码
	- `mysql` 自动给 `root` 用户设置随机密码，运行 `grep "password" /var/log/mysqld.log` 可以看到当前密码
9. 运行 `mysql -u root -p`，用 `root` 用户登录，提示输入密码使用上面查询到的，成功登录进 `mysql` 命令行![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221112190924.png)
10. 设置 `root` 密码，可以运行 `set global validate_password_policy=0;` 提示密码设置策略，（`validate_password_policy` 默认值为1，生产环境这个需要设置高级的）
11. `set password for 'root'@'localhost'=password('12345678');`
12. 运行 `flush privileges;` 使密码开始生效。
![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221112191718.png)