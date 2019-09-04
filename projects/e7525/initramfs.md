
/bin
	包括了很多基本命令：cat awk ln ls等,很多都是busybox链接

/dev
	两个块设备文件：
		console
		null

/etc
	各种配置文件是要的

/home
	两个文件夹（两个用户）：
		/root：有个ko文件夹：
			ko：有个网络驱动模块：
				mt7601Usta.ko
		/tsh：链接文件，链接到/mnt/app/目录下对应的程序
			start.sh文件，启动/mnt/app/autorun.sh
			

/lib
	/各种库文件
	/depmod.d
		/search.conf 文件
	/moudules
		/3.14.52+
			/kernel ：空
		/modules.alias等文件
	/udev
		/很多 *_id 的文件

/media
	空

/mnt
	/app	
		空	要挂载app.tar.bz2
	/boot	
		空
	/config	要挂载config.tar.bz2
		空
	/log	
		空
	/nfs	
		空
	/reserve	
		空

/proc
	空

/run
	空
	
/sbin
	命令

/sys
	空

/tmp
	空

/usr
	/share
		/usb.ids.gz 文件

/var
	/backups
	/cache
	/lib
	/local
	...
