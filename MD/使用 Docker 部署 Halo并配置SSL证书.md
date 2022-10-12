# 使用 Docker 部署 Halo

## 使用 Docker 镜像

**安装Docker**
本文使用全新安装的系统，因此并没有安装`Docker`，已安装`Docker`则可跳过这一步。登录终端输入以下内容并按回车等待即可完成`Docker`安装，该命令同样适用于`Ubuntu`。

```bash
curl -fsSL https://get.docker.com | bash -s docker --mirror Aliyun
```

`Halo` 在 `Docker Hub` 上发布的镜像为 [halohub/halo](https://hub.docker.com/r/halohub/halo)

1. 创建 [工作目录](https://docs.halo.run/getting-started/prepare#工作目录)

```bash
mkdir ~/.halo && cd ~/.halo
```

2. 下载示例配置文件到 [工作目录](https://docs.halo.run/getting-started/prepare#工作目录)

```bash
wget https://dl.halo.run/config/application-template.yaml -O ./application.yaml
```

3. 编辑配置文件，配置数据库或者端口等，如需配置请参考 [配置参考](https://docs.halo.run/getting-started/config)

```bash
vim application.yaml
```

4. 拉取最新的 Halo 镜像

```bash
docker pull halohub/halo:1.5.4
```

5. 创建容器

```bash
docker run -it -d --name halo -p 8090:8090 -v ~/.halo:/root/.halo --restart=unless-stopped halohub/halo:1.5.4
```

- **-it：** 开启输入功能并连接伪终端
- **-d：** 后台运行容器
- **--name：** 为容器指定一个名称
- **-p：** 端口映射，格式为 `主机(宿主)端口:容器端口` ，可在 `application.yaml` 配置。
- **-v：** 工作目录映射。形式为：-v 宿主机路径:/root/.halo，后者不能修改。
- **--restart：** 建议设置为 `unless-stopped`，在 Docker 启动的时候自动启动 Halo 容器。

6. 打开 `http://ip:端口号` 即可看到安装引导界面。



# 使用`Nginx`进行反向代理

> 注意下文内容基于使用`8090`宿主机端口，如有更改请注意在配置文件中将`8090`改为自行修改的端口



#### 安装`Nginx`

```bash
# 下列代码适用于CentOS 
# 添加 Nginx 源 
sudo rpm -Uvh  http://nginx.org/packages/centos/7/noarch/RPMS/nginx-release-centos-7-0.el7.ngx.noarch.rpm 

# 安装 Nginx 
sudo yum install -y nginx 

# 启动 Nginx 
sudo systemctl start nginx.service 

# 设置开机自启 Nginx 
sudo systemctl enable nginx.service

# 下列代码适用于Ubuntu 
sudo update sudo apt install nginx
```

配置Nginx

1. 



```bash
# 下载 Halo 官方的 Nginx 配置模板 
curl -o /etc/nginx/conf.d/halo.conf --create-dirs https://dl.halo.run/config/nginx.conf
```

下载之后需要对其进行修改。以上方法安装的`Nginx`默认路径为`/etc/nginx`

```bash
# 适用 vim 编辑 halo.conf 
vim /etc/nginx/conf.d/halo.conf
```

打开之后的内容应该类似

```bash
server {     
	listen 80;    
 	server_name example.com www.example.com; # 将 example.com www.example.com 修改为自己的域名   
    location / {         
    proxy_set_header HOST $host;         
    proxy_set_header X-Forwarded-Proto $scheme;         
    proxy_set_header X-Real-IP $remote_addr;        
    proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;         
    proxy_pass http://127.0.0.1:8090/; # 如有更改默认的宿主机8090端口，请修改此处为执行选择的端口   
    } 
}

```

修改完成之后

```bash
# 检查配置是否有误 
sudo nginx -t 

# 重载 Nginx 配置 
sudo nginx -s reload
```



# 使用 `certbot` 申请并自动安装SSL证书

阿里云/腾讯云等云服务商也可以申请免费的`SSL`证书并下载，这类证书请查阅相关教程，本文仅介绍通过`certbot`申请证书并自动安装。

1. 安装 `certbot` 和 `certbot nginx` 插件：

```bash
# 根据自己的系统选择相应命令 

# CentOS 安装 certbot 以及 certbot nginx 插件 
sudo yum install certbot -y 
sudo yum install python3-certbot-nginx -y 

# Ubuntu 安装 certbot 以及 certbot nginx 插件 
sudo apt install certbot 
sudo apt install python3-certbot-nginx
```

2. 申请并自动配置证书：

```bash
sudo certbot --nginx
```

需要输入邮箱并按y或a同意相关协议，具体请参考输入命令后的输出

3. 自动续约

这里申请的免费证书可以免费续期，理论上可以一直免费使用，这里提供了自动执行续期的命令

```bash
sudo certbot renew --dry-run
```



到这里，即完成了所有的步骤，可以直接通过域名进行Halo博客的访问。注意，国内服务商注册的域名大多需要备案，否则无法使用，具体请参考云服务商的文档。

在设置完反向代理后，必须在博客的后台管理界面设置正确的博客地址，否则可能导致CSS加载不成功、样式混乱等错误。

![Docker部署Halo博客并配置SSL证书_Docker](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/9d9dddde55e7081f419f264267b0815d.png)

