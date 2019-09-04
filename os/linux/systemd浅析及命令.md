


常用命令
======================================================
使某服务自动启动
systemctl enable httpd.service

使某服务不自动启动
systemctl disable httpd.service

检查服务状态
systemctl status httpd.service （服务详细信息） 
systemctl is-active httpd.service （仅显示是否 Active)

显示所有已启动的服务
systemctl list-units --type=service

启动某服务
systemctl start httpd.service

停止某服务
systemctl stop httpd.service

重启某服务
systemctl restart httpd.service

修改配置文件后重启
修改配置文件以后，需要重新加载配置文件，然后重新启动相关服务。

# 重新加载配置文件
$ sudo systemctl daemon-reload

# 重启相关服务
$ sudo systemctl restart foobar
======================================================








开机服务管理
======================================================
开机启动unit
systemctl enable test.service
增加由/lib/systemd/system/到/etc/systemd/system/multi-user.target.wants/下的软链接
ln -s '/usr/lib/systemd/system/postfix.service' '/etc/systemd/system/multi-user.target.wants/test.service'

一旦修改配置文件，就要让 SystemD 重新加载配置文件，然后重新启动，否则修改不会生效。
$ sudo systemctl daemon-reload
$ sudo systemctl restart httpd.service

开机不启动unit
systemctl disable test.service
删除/etc/systemd/system/multi-user.target.wants下的软链接

查看开机是否启动
systemctl is-enabled test.service #查询服务是否开机启动

systemd查看开机自启动的程序
ls /etc/systemd/system/multi-user.target.wants/

查看systemd单元加载及活动情况
systemctl

显示启动失败的单元
systemctl --failed

查看systemd管理的所有单元
systemctl list-unit-files
======================================================














服务管理
======================================================
启动服务
systemctl start httpd.service

关闭服务
systemctl stop httpd.service

重启服务
systemctl restart httpd.service

重新加载
systemctl reload httpd.service

查看状态
systemctl status httpd.service
包括启动状态、启动时间、主进程及相关进程、相关日志
======================================================






systemctl
======================================================
systemctl是 Systemd 的主命令，用于管理系统
# 重启系统
$ sudo systemctl reboot

# 关闭系统，切断电源
$ sudo systemctl poweroff

# CPU停止工作
$ sudo systemctl halt

# 暂停系统
$ sudo systemctl suspend

# 让系统进入冬眠状态
$ sudo systemctl hibernate

# 让系统进入交互式休眠状态
$ sudo systemctl hybrid-sleep

# 启动进入救援状态（单用户状态）
$ sudo systemctl rescue
======================================================





systemctl list-units命令可以查看当前系统的所有 Unit 。
======================================================
# 列出正在运行的 Unit
$ systemctl list-units

# 列出所有Unit，包括没有找到配置文件的或者启动失败的
$ systemctl list-units --all

# 列出所有没有运行的 Unit
$ systemctl list-units --all --state=inactive

# 列出所有加载失败的 Unit
$ systemctl list-units --failed

# 列出所有正在运行的、类型为 service 的 Unit
$ systemctl list-units --type=service
======================================================





======================================================
# 显示某个 Unit 是否正在运行
$ systemctl is-active application.service

# 显示某个 Unit 是否处于启动失败状态
$ systemctl is-failed application.service

# 显示某个 Unit 服务是否建立了启动链接
$ systemctl is-enabled application.service
======================================================






