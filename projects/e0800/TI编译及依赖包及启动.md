
Vision_sdk/linux/docs/VisionSDK_LinuxUserGuide.pdf
《VisionSDK_LinuxUserGuide.pdf》

编译前需要的依赖包
	：sudo apt-get install ia32-libs lib32stdc++6 lib32z1 lib32z1-dev
		uname, sed, mkimage, dos2unix, dtrx, mono-complete, git, corkscrew
		
		
编译源码
this will build kernel, u-boot and sgx drivers & memcache.ko
	第一次编译或者改变了u-boot/kernel/sgx drivers时
		$> cd $INSTALL_DIR/vision_sdk 
		$> make linux 
		$> make linux_install
	
	否则直接编译SDK
		$>make –s –j depend 
		$>make –s –j
		
		
编译后下列目录的东西将会更新
	$INSTALL_DIR/vision_sdk/linux/targetfs/lib/firmware
	$INSTALL_DIR/vision_sdk/linux/targetfs/opt/vision_sdk
	$INSTALL_DIR /vision_sdk/linux/boot
	$INSTALL_DIR /vision_sdk/linux/targetfs/boot
	
该目录下的文件系统当作NFS或SD卡文件系统
	$INSTALL_DIR/vision_sdk/linux/targetfs
	
复制文件系统
	$>sudo –s or $>sudo 
	root>export INSTALL_DIR=<installation_directory_absolute_path> 
	root>cd $INSTALL_DIR/vision_sdk/linux/targetfs 
	root>tar czvf arago-glsdk-multimedia-image-dra7xx-evm.tar.gz ./* 
	root>mv ./ arago-glsdk-multimedia-image-dra7xx-evm.tar.gz $INSTALL_DIR/vision_sdk/linux/boot/ 
	root>exit


制作SD卡（<parent_device_name> can be found using “mount” command）
	$>sudo –s or sudo
	root> bash
	root> export INSTALL_DIR=<installation_directory_absolute_path>
	root> cd $INSTALL_DIR/vision_sdk/linux/scripts
	root> ./mksdboot.sh --device /dev/<parent_device_name> --sdk $INSTALL_DIR/vision_sdk
	root> exit	

NFS only boot启动
	1. Copy zImage and dra7-evm-infoadas.dtb 
		from vision_sdk/linux/targetfs/boot to FAT partition in SD card
	2. Copy MLO, u-boot.img 
		from vision_sdk/linux/boot to SD card
	3. Boot EVM with SD card, 
		hit enter to get to u-boot prompt
	4. Do below at uboot prompt, edit NFS server IP and filesystem path to match your environment, 
		setenv bootargs 'console=ttyO0,115200n8 vram=16M root=/dev/nfs rw 
			nfsroot=172.24.170.60:/datalocal/user/abc/vision_sdk/linux/targetfs rootwait
			ip=dhcp mem=1024M' 
		setenv fdt_high 0x84000000 
		setenv bootcmd 'load mmc 0 0x825f0000 dra7-evm-infoadas.dtb;
			load mmc 0 0x80300000 zImage;bootz 0x80300000 - 0x825f0000' save
	5. Now reboot board, next time onwards just copy the zImage and .dtb to SD card, if it is updated, 
		and reboot board with SD card
		
SD only boot启动
	1、Copy uenv_sd.txt at $INSTALL_DIR/linux/scripts/ to $INSTALL_DIR/linux/boot
	2、Rename uenv_sd.txt at $INSTALL_DIR/linux/boot to uenv.txt
	3、Use dos2unix command on uenv.txt at $INSTALL_DIR/linux/boot 
		$> dos2unix $INSTALL_DIR/linux/boot/uenv.txt
	4、确认$INSTALL_DIR/linux/boot目录，出现下列文件：
		arago-glsdk-multimedia-image-dra7xx-evm.tar.gz
		MLO
		u-boot.img
		uenv.txt
	5、制作SD卡
	6、插卡启动
	
	
	
	
	
	
	
		