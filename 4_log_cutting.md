## 4.log_cutting ##

日志切割，有这样一个access.log每天会打出大量的日志。实现一个日志切割的功能，并说明该实现方式会有什么缺陷。



1. 直接用split切割，可以指定切割文件的行数或者大小等等

   命令如下

- split -b 50m access.log (以50M大小切割)

- split -l 300 access.log （每300行切割）

这样仅仅是将文件切割变小了而已，没有太多实际含义

2 每天切割一次

    #!/bin/bash
	LOG_PATH=/path/of/your/log
	YESTERDAY=${date -d "yesterday"+%Y-%m-%d}
	mv ${LOG_PATH}/access.log ${LOG_PATH}/access_${YESTERDAY}.log

将其命名为cut_log.sh,然后建立crontab定时任务

    0 0 * * * cut_log.sh

这样可以把每天产生的日志放入不同文件中，缺点是需要根据产生日志的应用程序令其每天重新将日志放入access.log中
