# Typora+PicGo+阿里云OSS服务

## Typora下载

下载`Typora`,目前`Typora`支持多平台安装，进入国内[官网](https://typoraio.cn/)，国外的太慢了，目前需要收费，89rmb即可拿下，若不想花钱，这里有[beta版](https://www.aliyundrive.com/s/26FApafqRFo),不过还是建议大家支持正版。（根据你的电脑选择具体版本），下载完先放着直接进行下一步。

![image-20220716132428443](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/image-20220716132428443.png)

## 购买阿里云OSS服务

1.前提是你得有一个[阿里云](https://www.aliyun.com/)账号，没有的直接注册就行，然后选择对象存储`OSS`，如果找不到直接在搜索栏搜索`OSS`，点击折扣套餐或者立即购买。

![image-20220716132941868](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/image-20220716132941868.png)

2.进入如下界面，资源包类型和地域不用管，存储包规格正常`40GB`完全够用了，购买时常自选，半年到5年不等，价格还是比较合适的，一年才`9rmb`，选择完成之后点击立即购买，然后付款完成。![image-20220716133240824](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/image-20220716133240824.png)

3.创建`Bucket`,还是进入`OSS`对象存储，如果找不到就搜索，进入管理控制台。名称自定义，后面要用，地域选择离自己近的，读写权限改为公共读，其他不用动，点击确定。

![image-20220716133643641](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/image-20220716133643641.png)

![image-20220716133819753](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/image-20220716133819753.png)

![image-20220716133917940](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/image-20220716133917940.png)

4.点击Bucket列表就可以看到你刚才创建的Bucket，点击概览

![image-20220716134206500](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/image-20220716134206500.png)

点击Bucket名称，进入Bucket管理

![image-20220716134251924](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/image-20220716134251924.png)

记住图中所指示的，我的是`vicent-picture-for-typora`和`oss-cn-beijing`。

![image-20220716134440259](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/image-20220716134440259.png)

点击文件管理，新建一个目录，我的是`img_for_typora/`。

![image-20220716134624472](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/image-20220716134624472.png)

5.创建`AccessKey`

鼠标放在右上角的图像上就出来了如下图，点击`AccessKey`管理

![image-20220716134847017](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/image-20220716134847017.png)

先点击继续使用`AccessKey`，然后再点击创建`AccessKey`。

![image-20220716135031692](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/image-20220716135031692.png)

创建完成后，复制`AccessKey` ID和`AccessKey Secret`。

![image-20220716151419938](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/image-20220716151419938.png)

## PicGo下载

可以去[官方](https://github.com/Molunerfinn/PicGo/releases/tag/v2.3.0)下载，选择对应的版本，我的是`windows64`,选择如下图。

如果`github`访问不了，可以自取[安装包](https://www.aliyundrive.com/s/ViQCSDpgcHL)

![image-20220716135416220](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/image-20220716135416220.png)

直接点击安装，成功界面如下

![image-20220716135601939](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/image-20220716135601939.png)

点击图床设置，然后点击阿里云`OSS`，

![image-20220716135646219](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/image-20220716135646219.png)

这里的设定`KeyId`将之前的`AccessKey ID`复制过来

设定`KeySecret`将之前的`AccessKey Secret`复制过来

设定存储空间名就是下图中的1，之前2.4的设置

确认存储区域就是下图中的2，之前2.4的设置

存储路径为之前新建目录名

然后点击确定，设置为默认图床

![image-20220716135754708](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/image-20220716135754708.png)

![image-20220716134440259](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/image-20220716134440259.png)

## Typora配置

点击`文件->偏好设置->图像`按照如下图进行设置，其中`PicGo`路径为之前安装`PicGo`的路径

![image-20220716140530117](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/image-20220716140530117.png)

至此所有的步骤都已经配置完成，可以直接再`Typora`中将图片上传到图床了。

## 注意

此时上传图片或者点击验证图片上传选项会报错`Failed to fetch`，如下图：

![image-20220716140916800](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/image-20220716140916800.png)

![image-20220716140951180](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/image-20220716140951180.png)

报错原因：如上图所示，Typora端口使用的是`36677`，而`PicGo`使用的端口是`36678`，此时只需要将`PicGo`的端口号改为`36677`即可，如下图所示：

打开PicGo选择`PicGo`设置，设置监听端口为`36677`，问题解决。此时你如果点击验证图片上传选项仍然报错，没有关系，图片已经能够上传了，这可能是一个`typora`的`bug`。

![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/image-20220716141120231.png)

# `PicGo` + `OSS对象存储` + `Obsidian`

前面已经配置好了 `PicGo`和`OSS`+`Typora`,但是由于现在`Typora`收费了,不想付费又不想用盗版可以使用`Obsidian`

设置`obsidian`就简单了,打开`obsidian` --- 设置 --- 第三方插件市场 --- 下载 `Image auto upload Plugin`

![image-20221010211148628](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/image-20221010211148628.png)



安装,启用选项中---配置如下设置

![image-20221010211248629](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/image-20221010211248629.png)



然后就可以愉快地使用了~











