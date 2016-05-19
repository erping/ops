## 11.vssh ##
在对单台机器做操作时我们经常会用“ssh ip”的方式登录到一台服务器上，能不能编写这样一个工具vssh ip1,ip2,...ipn来模拟登录到n台服务器，登录后所有操作相当于同时对n台服务器生效。


利用python中的paramiko模块，实现ssh登录，将要执行的命令写入cmd列表中，利用多线程并发执行，效率较高

	import paramiko
	import threading
    def vssh(ip,username,passwd,cmd):
		try:
			ssh = paramiko.SSHClinet()
			ssh.set_missing_host_key_policy(paramiko.AutoAddPolicy())
			ssh.connect(ip,22,username,passwd,timeout=10)
			for m in cmd:
				stdin,stdout,stderr = ssh.exec_command(m)
				out = stdout.readlines()
				for o in out:
					print o
			print '%s\tOK\n' %(ip)
			ssh.close()
		expect:
			print '%s\tError\n' %(ip)
	
	if __name__=='__main__':
		cmd = ['ls','apt-get -y install node.js'] #command list
		username = "root"
		passwd = ""
		for i in range(1,254):
			ip = '192.168.1.'+str(i)
			t = threading.Thead(target=vssh,args=(ip,username,passwd,cmd))
			t.start()