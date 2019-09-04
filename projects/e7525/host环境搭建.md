

主机基础环境安装脚本
```c
#!/bin/bash      
#Needed packages:
sudo apt-get install gettext libgtk2.0-dev rpm bison m4 libfreetype6-dev
sudo apt-get install libdbus-glib-1-dev liborbit2-dev intltool
sudo apt-get install ccache ncurses-dev zlib1g zlib1g-dev gcc g++ libtool
sudo apt-get install uuid-dev liblzo2-dev
sudo apt-get install tcl dpkg
sudo apt-get install asciidoc texlive-latex-base dblatex xutils-dev
sudo apt-get install texlive texinfo
sudo apt-get install lib32z1 lib32ncurses5 lib32bz2-1.0
sudo apt-get install libc6-dev-i386
sudo apt-get install u-boot-tools
sudo apt-get install scrollkeeper
 
sudo ln -s /usr/lib/x86_64-linux-gnu/librt.so   /usr/lib/librt.so
 
#Useful tools:
sudo apt-get install gparted
sudo apt-get install nfs-common nfs-kernel-server
sudo apt-get install git-core git-doc git-email git-gui gitk
sudo apt-get install meld atftpd
```


交叉编译环境安装
一、安装交叉编译工具fsl-imx-fb-glibc-x86_64-meta-toolchain-qt5-cortexa9hf-vfp-neon-toolchain-3.14.52-1.1.0

	$ chmod +x fsl-imx-fb-glibc-x86_64-meta-toolchain-qt5-cortexa9hf-vfp-neon-toolchain-3.14.52-1.1.0.sh
	$ sudo ./fsl-imx-fb-glibc-x86_64-meta-toolchain-qt5-cortexa9hf-vfp-neon-toolchain-3.14.52-1.1.0.sh
	
	
二、安装lzo
	1、tar -zxvf lzo-2.06.tar.gz
	2、mv lzo-2.06 lzo
	3、cd lzo
	4、export CFLAGS=-m64
	5、sudo ./configure -enable-shared
	6、sudo make
	7、sudo make install(默认安装在/usr/local/lib下：liblzo2.a liblzo2.la liblzo2.so liblzo2.so.2 liblzo2.so.2.0.0)
	8、在/etc/ld.so.conf.d/目录下新建文件lzo.conf，内容如下
	/usr/local/lib
	9、让lzo.conf生效：/sbin/ldconfig -v
	
	
三、安装lzop
	1、解压lzop-1.03.tar.gz
	2、配置 sudo ./configure CPPFLAGS=-I/usr/local/include LDFLAGS=-L/usr/local/lib
	3、编译 sudo make
	4、安装 sudo make install