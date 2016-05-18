## 1.password_cache ##


运维操作在很多情况下需要访问不同的服务器，运维人员可能会频繁的输入自己的账号和密码。
是否可以通过一个简单方式只需要输入一遍密码，然后余下的操作都可以不再重复的输入密码。
密码应该存储在什么地方会比较隐蔽，让有这台机器sudo权限的其他人看不到。（可以不写代码，回答便可）

设置ssh免密码登录，即在本地利用ssh-keygen -t rsa命令生成公钥和私钥，然后将公钥拷贝到需要登录的机器上并将其加入到authorized_keys中并设置600权限。大概命令如下
1. ssh-keygen -t rsa
2. scp id_rsa.pub root@remote_ip:~/.ssh/
3. cat id_rsa.pub >> ~/.ssh/authorized_keys
4. chmod 600 authorized_keys

密码的存储位置我的理解是配置/etc/sudoer里sudo用户的权限，使其不能进入私钥所在目录。