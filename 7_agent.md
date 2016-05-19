实现一个被控程序，连接对应的端口便可以对被控端输送命令。
这是一个可以重复调用的服务，不能把bash的io直接绑到tcp上。命令运行完后命令的输出应该能返回到控制机的STDOUT。（考察tcp，多线程等）

建立TCP连接被控端，读取输入后返回输出到STDOUT
    import socket
	s = socket.socket(socket.AF_INET,socket.SOCK_STREAM)
	s.connect(('ipaddr',PORT))
	while True:
		command = input("please input the command")
		s.send(command)
		buff = []
		while True:
			d = s.recv(1024)
			if d:
				buff.append(d)
			else:
				break
		data = b''.join(buffer)
		print data
	s.close