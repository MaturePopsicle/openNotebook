1、samba的安装
$ apt-get install samba samba-common smbclient 
//保存现有的配置文件
$ cp /etc/samba/smb.conf /etc/samba/smb.conf.bak

2、Samba配置
$ vim /etc/samba/smb.conf
在文件 smb.conf 最后追加
# Add by Tony for Samba && tftpd
[tony]
   path = /home/tony
   available = yes
   browseable = yes
   writable = yes

[tftpboot]
   path = /home/tony/tftpdir
   available = yes
   browseable = yes
   writable = yes
   public = yes

[opt]
   path = /opt
   available = yes
   browseable = yes
   writable = yes
   public = yes

上面 tony 是用户名，不能有“#”符号

3、创建samba帐户
$ smbpasswd -a USERNAME (USERNAME换成你的用户名)
会要求你输入samba帐户的密码
New SMB password:
Retype new SMB password:
［ 如果没有这一步， 当你登录时会提示 session setup failed:
NT_STATUS_LOGON_FAILURE

4、重启samba服务器
$ /etc/init.d/smbd reload (修改过smb.conf的话要执行一次)
$ /etc/init.d/smbd restart

5、测试
可以到windows下输入ip试一下了
在文件夹处输入 "\\" + "Ubuntu机器的ip或主机名"
Ubuntu 14.04 访问Window XP下的文件
直接在地址栏中输入 "smb://1XP机器的ip地址/

6、开机随机自启动
如上配置，如果重启机器samba将不可以使用，需要配置系统随机启动服务
$ apt-get install -y sysv-rc-conf
$ sysv-rc-conf 
配置 smbd   samba   nmbd 服务 等级 1到5