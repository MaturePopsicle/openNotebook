一.编译触屏库tslib1.4(touch screen lib)
	1.把压缩包拷贝到Ubuntu,解压
		tar xvf tslib-1.4.tar.gz 
 
	2.cd tslib	
		要确保安装以下工具：
			sudo apt-get install autoconf
			sudo apt-get install automake
			sudo apt-get install libtool

		安装完成后，执行以下脚本：
		 ./autogen.sh 
		执行成功会生成 configure 文件
		
	3.检查配置
		./configure --prefix=/usr/local/tslib --host=arm-linux ac_cv_func_malloc_0_nonnull=yes
		
		注：上述命令中malloc后面的是数字0，不是字母O
		配置成功生Makefile文件

	4.make
		make 正确执行后显示如下：
		make[2]: Leaving directory `/home/csgec/software/tslib/tests'
		make[2]: Entering directory `/home/csgec/software/tslib'
		make[2]: Leaving directory `/home/csgec/software/tslib'
		make[1]: Leaving directory `/home/csgec/software/tslib'
		
	可能出现的错误：
		...
		  __open_missing_mode ();
		...
		解决方案：
			vim tests/ts_calibrate.c 
			搜索open,227行左右
			给open函数加上第三个参数
			 if ((calfile = getenv("TSLIB_CALIBFILE")) != NULL) {
             cal_fd = open (calfile, O_CREAT | O_RDWR,0777);
			 } else {
				 cal_fd = open ("/etc/pointercal", O_CREAT | O_RDWR    ,0777);                                                       
			 }


			
	5.sudo make install
	
		检查最后结果是否正确：
		file /usr/local/tslib/bin/ts_test 
		/usr/local/tslib/bin/ts_test: ELF 32-bit LSB  executable, ARM, EABI5 version 1 (SYSV), dynamically linked (uses shared libs), for GNU/Linux 2.6.16, not stripped

二.编译QT库
	1.解压最新版的交叉编译器(4.8.3)
		tar xvf arm-2014.05-29-arm-none-linux-gnueabi-i686-pc-linux-gnu.tar.bz2 
		
		编译器所在路径：
		/home/csgec/software/arm-2014.05/bin/
		
		编译器完整名称：
			arm-none-linux-gnueabi-g++
			...

	2.解压QT源码包：
		tar xvf qt-everywhere-opensource-src-5.6.0.tar.gz 

		cd qt-everywhere-opensource-src-5.6.0/

	3.删除3D模块
		rm qt3d/ qtweb* -rf
	
	4.修改编译器
		vim qtbase/mkspecs/linux-arm-gnueabi-g++/qmake.conf 

----------------------------------------------------
#tslib path  添加的
 14 QMAKE_INCDIR += /usr/local/tslib/include
 15 QMAKE_LIBDIR += /usr/local/tslib/lib
 16 #platform 添加的
 17 QT_QPA_DEFAULT_PLATFORM = linuxfb
 18 #cpu 添加的
 19 QMAKE_CFLAGS_RELEASE += -O2 -march=armv7-a
 20 QMAKE_CXXFLAGS_RELEASE += -O2 -march=armv7-a
 21 
 22 # modifications to g++.conf 修改
 23 QMAKE_CC                = /home/csgec/software/arm-2014.05/bin/arm-none-linux-gnueabi-gcc
 24 QMAKE_CXX               = /home/csgec/software/arm-2014.05/bin/arm-none-linux-gnueabi-g++
 25 QMAKE_LINK              = /home/csgec/software/arm-2014.05/bin/arm-none-linux-gnueabi-g++
 26 QMAKE_LINK_SHLIB        = /home/csgec/software/arm-2014.05/bin/arm-none-linux-gnueabi-g++
 
 28 
 29 # modifications to linux.conf	修改
 30 QMAKE_AR                = /home/csgec/software/arm-2014.05/bin/arm-none-linux-gnueabi-ar cqs
 31 QMAKE_OBJCOPY           = /home/csgec/software/arm-2014.05/bin/arm-none-linux-gnueabi-objcopy
 32 QMAKE_NM                = /home/csgec/software/arm-2014.05/bin/arm-none-linux-gnueabi-nm -P
 33 QMAKE_STRIP             = /home/csgec/software/arm-2014.05/bin/arm-none-linux-gnueabi-strip
 34 load(qt_config)



	5.检查配置
./configure  -release -opensource -xplatform linux-arm-gnueabi-g++ -prefix /usr/local/qtlib5.6.0 -silent -tslib -qt-sql-sqlite -no-opengl -no-dbus -no-iconv -nomake examples -nomake tools -nomake tests

	如果正常，显示如下：
	Qt is now configured for building. Just run 'make'.
	Once everything is built, you must run 'make install'.
	Qt will be installed into /usr/local/qtlib5.6.0
	
	生成Makefile
	
	6.make
	7.sudo make install

	8.打包生成的QT库和插件
		cd /usr/local/qtlib5.6.0
		sudo mkdir Qt2ArmLibandPlugin
		sudo cp lib/ plugins/ Qt2ArmLibandPlugin/ -rf
		sudo tar zcvf qtLib5.6.0.tar.gz Qt2ArmLibandPlugin/
		
		cp qtLib5.6.0.tar.gz ~/tftp/
		sudo service tftpd-hpa restart 

	9.把生成的压缩包下载到开发板
			
	10.打包触屏库，并下载到开发板
		cd /usr/local/tslib
		sudo mkdir myTslib
		sudo cp lib/ myTslib/ -rf
		sudo tar zcvf tslib1.4.tar.gz myTslib/
		
		
	12.qt creator配置
		1.打开qtcreator 找到菜单(工具)-->选项
		2.默认进入Build&Run
			a.添加编译器(Complier)
			add->GCC->Complier path(最新版本的编译器所在目录，选arm-xxx-g++)
			点击应用完成
			b.添加版本(即编译生成的qmake)
			add->qmake所在目录(/usr/local/qtlib5.6.0/bin)
			详情显示：
				Qt Version 5.6.0 for Embeded Linux
				
			点击应用完成
		3.添加工具包(Kits)
			点击add
			修改Name、Compiler、Qt version
			点击完成
		
		4.构建工程时，选择刚添加的ARM工具包，选release
		5.不要直接运行，只要构建就可以了
		6.把生成的可执行程序下载到开发板
	

	13.开发板环境配置
	vim qtconf.sh
		
		#!/bin/bash

		#动态库路径设置
		export QTHOME=/home/Qt2ArmLibandPlugin
		export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:$QTHOME/lib

		#平台
		export QT_QPA_PLATFORM_PLUGIN=$QTHOME/plugins
		export QT_QPA_PLATFORM=linuxfb::tty=/dev/fb0

		#触屏
		export QT_PLUGIN_PATH=$QTHOME/plugins
		export QT_QPA_GENERIC_PLUGINS=tslib
		export LD_PRELOAD=$QTHOME/lib/libts.so

		#字体
		export QT_QPA_FONTDIR=$QTHOME/font

	14.使上述脚本生效
		source qtconf.sh
		执行QT文件 
		./Test560





六、Ubuntu14.04中QTcreator无法输入中文的问题（好像并没有什么用iBus框架好像不需要修改什么就能支持中文）
		iBus框架

		将/usr/lib/x86_64-linux-gnu/qt5/plugins/platforminputcontexts/目录中
		的libibusplatforminputcontextplugin.so复制到qtcreator安装目录
		例如：
			sudo cp /usr/lib/x86_64-linux-gnu/qt5/plugins/platforminputcontexts/libibusplatforminputcontextplugin.so 
				/Tools/QTcreator/bin/plugins/platforminputcontexts(作用是使得qtcreator开发环境支持输入法)



七、QT5.6.0安装 及环境配置



