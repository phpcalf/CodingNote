# 定时清理 历史遗留文件

	麻麻再也不用担心我 服务器存储空间不足了。
	

## 第一步 ，清理 前N天的 文件  第二步，加入定时任务 


### 查询 /home/ojbk/images/ 中 文件后缀为.jpg 且时间为5天以前的 图片将其删除 
>find /home/ojbk/images/ -mtime +5 -name "*.jpg" -exec rm -rf {} \;

### 总不能每次都手动执行上面这条命令吧这样太麻烦了
	
	于是我们把它加入到定时任务中 使用 crontab -e 
	
>2 0 * * * /bin/find /home/ojbk/images/ -mtime +5 -name "*.jpg" -exec rm -rf {} \;

上面这条命令说的是 每天凌晨0点2分  删除/home/ojbk/images/中 前 5天的 jpg 图片


##删除命令 

>find 对应目录 -mtime +天数 -name "文件名" -exec rm -rf {} \;


|参数|作用|
|:-|:-|
|find|查找命令 |
|/home/ojbk/images/|想要进行清理的目录，这里只是示例目录|
|-mtime|限定的时间|
|+5| 前5天   写成 -1 就是包括今天|
|"*.jpg"|图片文件，所有文件的话就是将jpg换成* 就好了|
|-exec rm -rf {} \;|删除命令 |
	
## 定时任务   

	* * * * * command 


####这前面 的 五个  * 代表什么意思呢?
	
>答：分别代表  分钟、小时、 日期、月份、星期几  这里参数全是1 说明这个定时任务 1分钟执行一次

>>分钟，可以是从0到59之间的任何整数
>>小时，可以是从0到23之间的任何整数。
>>日期，可以是从1到31之间的任何整数。
>>月份，可以是从1到12之间的任何整数。
>>星期几，可以是从0到7之间的任何整数，这里的0或7代表星期日。
>>command：要执行的命令，可以是系统命令，也可以是自己编写的脚本文件。

	当然 你可以把 一系列的命令写到shell脚本中 通过这个
	
>crontab -e 

	加入到定时任务中 

>>星号（*）：代表所有可能的值，例如month字段如果是星号，则表示在满足其它字段的制约条件后每月都执行该命令操作。

>>逗号（,）：可以用逗号隔开的值指定一个列表范围，例如，“1,3,5,7”

>>横杠（-）：可以用整数之间的中杠表示一个整数范围，例如“1-5”表示“1,,2,3,4,5”

>>斜线（/）：可以用正斜线指定时间的间隔频率，例如“0-23/2”表示每两小时执行一次,同时正斜线可以和星号一起使用,例如*/10，如果用在minute字段，表示每十分钟执行一次。

|示例|作用|
|:-|:-|
|6,12 * * * *|每小时的第6分钟和第12分钟执行 |
|6,12 5-6 * * * |在上午5点到6点的第6和第12分钟执行|
|6,12 5-6 */6 * * |每隔两天执行一次，具体执行时间为上午5点到6点的第6和第12分钟|
|5 3 * * 6,0| 每周六周日3点5分执行|


