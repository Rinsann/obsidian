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

