## 6.sysinfo_recorder ##
写一个本地服务，定时的搜集系统的cpu使用情况并记录下来。
需要考虑到cup的使用情况包括哪项信息，用什么方式存储数据（记录文件的大小不能一直增长，记录的数据易于展示）。


利用crontab，每分钟记录top命令中cup那行数据，每天备份一下并删除原文件，每周删除一下备份文件

编辑crontab文件，crontab -e

    */1 * * * * echo -n $(date +%Y-%m-%d-%H-%M) >>/var/cpuinfo.log && top -n 1 |grep "Cpu" >>/var/cpuinfo.log
	* * */1 * * cat /var/cpuinfo.log >> /var/cpuinfo_backup.log && rm /var/cpuinfo.log
	*  * */7 * * rm /var/cpuinfo_backup.log