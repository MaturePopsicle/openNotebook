

$ cat /proc/partitions		/*查看sd卡信息*/

$ sudo dd if=u-boot-mx6q-sabresd.bin of=/dev/sdb bs=512 seek=2 skip=2 conv=fsync

$ sudo dd if=uImage of=/dev/sdb bs=512 seek=2048 conv=fsync

$ sudo fdisk /dev/sdb
	u [switch the unit to sectors instead of cylinders]
		其中'u'是在sectors和cylinders模式之间切换。此处应切换为sectors。
	d [repeat this until no partition is reported by the 'p' command ]
	n [create a new partition]
	p [create a primary partition]
	1 [the first partition]
	16384 [starting at offset sector #16384, i.e. 8MB, which leaves enough space for the
			kernel, the boot loader and its configuration data]
	<enter> [using the default value will create a partition that spans to the last sectorof the medium]
	w [ this writes the partition table to the medium and fdisk exits]
	其中'u'是在sectors和cylinders模式之间切换。此处应切换为sectors。

$ sudo mkfs.ext4 /dev/sdb1


$ mkdir /home/user/mountpoint
$ sudo mount /dev/sdb1 /home/user/mountpoint


$ gunzip rootfs.ext2.gz
$ mount -o loop -t ext2 rootfs.ext2 /home/user/rootfs


$ cd /home/user/rootfs
$ sudo cp -a * /home/user/mountpoint
$ sudo umount /home/user/mountpoint

