### `Crond` 任务调度
`crontab` 进行定时任务的设置
![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221111105829.png)

**概述**
任务调度：是指系统在某个时间执行的特定的命令或程序
任务调度分类：
	- 系统工资：有些重要的工作必须周而复始的执行，比如病毒扫描
	- 个别用户工作：个别用户可能希望执行某些程序，比如对`mysql`数据库的备份

**基本语法**
- `crontab [选项]`

**常用选项**
- `-e`：编辑`crontab`定时任务
- `-l`：查询`crontab`任务
- `-r`：删除当前用户的所有的`crontab`任务

**快速入门**
- 设置任务调度文件：`/etc/crontab`
- 设置个人任务调度，执行`crontab -e` 命令
- 接着输入任务到调度文件
- 比如，每小时的每分钟执行`ls -l /etc/ > /tmp/to.txt` 命令：
	- `*/1 * * * * ls -l /etc/ > /tmp/to.txt`

**参数细节说明**
5个占位符的说明
- 第一个`*`：一小时当中的第几分钟（范围0-59）
-  第二个`*`：一天当中的第几小时（范围0-23）
-  第三个`*`：一个月当中的第几天（范围1-31）
-  第四个`*`：一年中的第几个月（范围1-12）
-  第五个`*`：一周中的星期几（范围0-7,0和7都代表星期日）

**特殊符号的说明**
![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221111105232.png)

**特定时间执行任务案例**
![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221111105422.png)

**示例：**
- 每隔一分钟，就将当前的日期信息，追加到 `/tmp/mydate` 文件中
	- 脚本 `*/1 * * ** date >> /tmp/mydate`
- 每个一分钟，将当前日期和日历都追加到 `/home/mycal` 文件中
	- `vim /home/my.sh` 
	- `date >> /home/mycal`
	- `cal >> /home/mycal`
	- 给 `my.sh` 增加执行权限，`chmod u+x /home/my.sh`
	- `crontab -e`
	-  `*/1 * * * * /home/my.sh`
- 每天凌晨2:00 将`mysql`数据库`testdb`，备份到文件中。
	- `crontab -e`
	- `0 2 * * * mysqldump -u root -proot testdb > /home/db.bak`

![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221111110238.png)

![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221111110032.png)
![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221111110422.png)

**`crond` 相关指令**
- `crontab -r`：终止任务调度
- `crontab -l`：列出当前有哪些任务调度
- `service crond restart`：重启任务调度

### `at` 定时任务
**基本介绍**
1. `at` 命令是一次性定时计划任务，`at` 的守护进程 `atd` 会以后台模式运行，检查任务队列来运行。
2. 默认情况下，`atd` 守护进程每60秒检查任务队列，有任务时，会检查任务运行时间，如果时间与当前时间匹配，则运行此任务。
3. `at` 命令是一次性定时计划任务，执行完一个任务后不在执行此任务了
4. 在使用 `at` 命令的时候，一定要保证 `atd` 进程的启动，可以使用相关指令查看
	1. `ps -ef | grep atd` 检测当前正在运行的进程，并过滤出来`atd`的

**`at` 命令格式**
- `at [选项] [时间]`
- `Ctrl + D` 结束 `at` 命令的输入

![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221111114203.png)

**at 命令选项**
![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221111114307.png)

**at 时间定义方法**
1. 接受在当天的 `hh:mm` （小时:分钟）式的时间指定，假如该时间已经过去，那么会放在第二天执行，例如：`04:00`
2. 使用 `midnight`（深夜），`noon`（中午），`teatime`（饮茶时间，一般是下午四点）等比较模糊的词语来指定时间
3. 采用`12`小时计时制，即在时间后面加上`AM`（上午）或`PM`（下午）来说明是上午还是下午，例如：`12PM`
4. 指定命令执行的具体日期，指定格式为`month day`（月 日）或 `mm/dd/yy`（月/日/年）或 `dd.mm.yy`（月.日.年），指定的日期必须跟在指定时间的后面，例如：`04:00 2022-12-25`
5. 使用相对计时法，指定格式为：`now+count time-units`，`now`就是当前时间，t`ime-units`是时间单位，这里能够是 `minutes`（分钟）、`hours`（小时）、`days`（天）、`weeks`（星期）。`count` 是时间的数量，几天，几小时，例如：`now + 5 minutes`
6. 直接使用`today`（今天）、`tomorrow`（明天）来指定完成命令的时间。

**示例**
- 两天后的下午五点执行 `/bin/ls /home`![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221111115522.png)
- `atq` 命令来查看系统中没有执行的工作任务![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221111115754.png)
- 明天17点钟，输出时间到指定文件内 比如：`/root/date100.log`![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221111115928.png)
- 2分钟后，输出时间到指定文件内：`/root/date200.log`![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221111120243.png)
- 删除已经设置好的任务，`atrm 编号`![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221111120752.png)
- 也可以执行脚本![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221111120910.png)

> 输入完命令后按两次 `Ctrl+D`结束，输错可以按 `Ctrl+Backspace` 删除