


查看CPU温度：
	打印 cat
	/sys/class/thermal/thermal_zone0

	trip_point_0_temp	温度
	trip_point_0_type	类型：critical降频、passive重启
	trip_point_1_temp	
	trip_point_1_type

	cat temp 	打印当前温度

设置重启温度：
	echo value x1000 > trip_point_*_temp

	pwd/mode
		echo disable 关闭 mode
			 enable 重启 mode


vi /etc/init.d/rc.local 开机启动文件


Linux中查看		cat /proc/cmdline  类似于 bootcmd

uboot之后  print 会打印出 boot相关信息