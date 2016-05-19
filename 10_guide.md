编写一个服务，用于查询之前定义好的信息。如在服务器端定义了foo=2014 那么客户端可以通过foo得到2014这个数据.

在服务器端的字典里定义好查询信息，然后建立TCP等待查询，收到查询关键字后从字典中取出value，如果不存在返回no such value

    import socket
	import threading
	d = {'foo':2014,'bar':2048}
	s = socket.socket(socket.AF_INET,socket.SOCK_STREAM)
	s.bind(("ipaddr",8888))
	s.listen(7)
	while True:
		sock, addr = s.accept()
		t = threading.Thread(target=search,args=(sock,addr))
		t.start()

	def search(sock,addr):
		while True:
			data = sock.recv(1024)
			if not data or data.edcode('utf-8) == 'exit':
				break
			if data.decode('utf-8') in d:
				sock.send(('%s', %d[data.decode('utf-8')].encode('utf-8')
			else
				sock.send(b'no such value')
		sock.close()