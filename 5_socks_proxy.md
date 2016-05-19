
##5.socks_proxy  ##

假设您有一个远端服务器可以通过ssh登录，在你的本地电脑上实现一个简单的socks代理服务，可以在断网或重起的情况下重新建立连接。（提示：ssh tunnel）

利用ssh的-D参数实现socks代理,socks_proxy.sh

    #！/bin/bash	
	read -p "Please input the local port number:" LOCAL_PORT
	read -p "Please input the username of remote server:" REMOTE_USERNAME
	read -p "Please input the IP of remote server:" REMOTE_IP
	ssh -qTf -D 127.0.0.1:$LOCAL_PORT $REMOTE_USERNAME@$REMOTE_IP

对其添加执行权限

    chmod +x socks.sh

为了实现断网重连需要将脚本放在/etc/network/if-up.d/下（Debian/Ubuntu),/etc/sysconfig/network/if-up.d/下(openSUSE)

为了实现重启重连需要在/etc/rc.local中添加执行socks_proxy脚本
