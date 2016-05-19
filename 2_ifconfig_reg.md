## 2.ifconfig_reg ##

解析ifconfig命令的标准输出，返回一个hash。key是网卡名称 value是对应的ip。

如果确定只有一个网卡，比较好处理，命令如下

echo "eth0 `ifconfig eth0|grep "inet addr"|awk '{print $2}'| awk -F ":" '{print $2}'`" 

如果不确定网卡数量，脚本如下

    #!/bin/bash
	#get the number of NIC
    i=`ifconfig | sed -n "/eth[0-9]/p" |wc -l`
	declare -a hash
	#find the ip of ethi
	for((j=0;j<i;j++))
	do
	hash[$j]=`ifconfig eth$j |grep "inet addr"|   
	awk '{print $2}'|awk -F ":" '{print $2}'`
	done 
	#tranverse the array and output key value
	for element in ${!hash[*]}
	do
	  echo eth$element:${has[$element]}
	done 



