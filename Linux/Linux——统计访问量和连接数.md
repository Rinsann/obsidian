### 分析日志 `t.log`（访问量），将各个 `ip` 地址截取，并统计出现次数，从大到小排序

```bash
http://192.168.200.10/index1.html
http://192.168.200.10/index2.html
http://192.168.200.20/index1.html
http://192.168.200.30/index1.html
http://192.168.200.40/index1.html
http://192.168.200.10/order.html
```
![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221115123305.png)
```bash
cat t.log | cut -d '/' -f 3 | sort | uniq -c | sort -nr
```
### 统计连接到服务器的各个 `ip` 情况，并按连接数从大到小排序
![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221115123516.png)
```bash
 netstat -an | grep ESTABLISHED | awk -F " " '{print $5}' | awk -F ":" '{print $1}' | sort | uniq -c | sort -nr
```

![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221115123909.png)


# Linux——找回 MySQL 的 root 密码

## 忘记了 mysql5.7 数据库的 ROOT 用户密码，如何找回呢

```bash
vim /etc/my.conf
```
![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221115124433.png)
```bash
service mysqld restart # 重启服务
mysql -u root -p # 不输入密码直接回车
```

修改mysql密码
```sql
use mysql;
update user set authentication_string=password("rinhello") where user='root';
flush privileges;
exit
```

再次打开 `vim /etc/my.conf`，注释之前写的那句话。
![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221115124939.png)


重启 `mysql` 服务 `service mysqld restart`
再次进入 `mysql` 就可以使用修改后的密码了。