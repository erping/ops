## some questions of 360 ops ##



-  password_cache:

	运维操作在很多情况下需要访问不同的服务器，运维人员可能会频繁的输入自己的账号和密码。
	是否可以通过一个简单方式只需要输入一遍密码，然后余下的操作都可以不再重复的输入密码。
	密码应该存储在什么地方会比较隐蔽，让有这台机器sudo权限的其他人看不到。（可以不写代码，回答便可）

- ifconfig_reg:

	解析ifconfig命令的标准输出，返回一个hash。key是网卡名称 value是对应的ip。

- cron_ctrl:

	在一些环境中我们会用到crontab来做定时任务，但是有些情况下我们会暂时的关闭某个定时任务。
	能不能有这样一个操作界面方便的操作这些任务：
	./cron_ctrl jobname1 --stop ;./cron_ctrl jobname1 --start;./cron_ctrl jobname1 --list;
	编写一个工具来实现它。

- log_cutting：

	日志切割，有这样一个access.log每天会打出大量的日志。实现一个日志切割的功能，并说明该实现方式会有什么缺陷。

- socks_proxy:

	假设您有一个远端服务器可以通过ssh登录，在你的本地电脑上实现一个简单的socks代理服务，可以在断网或重起的情况下重新建立连接。（提示：ssh tunnel）

- sysinfo_recorder :

	写一个本地服务，定时的搜集系统的cpu使用情况并记录下来。
	需要考虑到cup的使用情况包括哪项信息，用什么方式存储数据（记录文件的大小不能一直增长，记录的数据易于展示）。

- agent： 

	实现一个被控程序，连接对应的端口便可以对被控端输送命令。
	这是一个可以重复调用的服务，不能把bash的io直接绑到tcp上。命令运行完后命令的输出应该能返回到控制机的STDOUT。（考察tcp，多线程等）

- dancer：

	用perl中的web框架dancer实现一个简单的功能。在web端能展示一个table，table有两列，分别是你指定的一个目录下面的文件的时间和文件名。
	需要考虑把获取数据和展示分离，不要直接print这个table的整个html字符串。

- group：

	实现一个树形结构的存取，编写一个类，这个类里面最少应有两个方法 add和get。
	add（k,v）: k:是父节点，v是子节点。
	my @nember = get( k )： 通过父节点返回这个父节点下的所以的叶子节点。

- vssh：

	在对单台机器做操作时我们经常会用“ssh ip”的方式登录到一台服务器上，能不能编写这样一个工具vssh ip1,ip2,...ipn来模拟登录到n台服务器，
	登录后所有操作相当于同时对n台服务器生效。

-  mrsync：

	从一组机器把数据拷贝到另一组机器上。
	为了尽量让拷贝的过程发生在一个交换机或者机房内，拷贝的时候源ip和目标ip尽量的相近（如: 10.1.1.1 和 10.1.1.2相近）。
	拷贝的目标机器和源机器可能有坏的情况，拷贝过程中有错误的机器就放弃（拷贝函数出错会有一个错误的返回码）。
	描述一个算法，怎样可以尽量的让拷贝发生在相近的ip上，又能大量的并发（已经有数据的机器都可以作为源机器）。
	（尽量不要跨机房拷贝，ip在分配的时候不同机房相差会比较大，如A机房是10.1.x.x B机房是10.9.x.x）