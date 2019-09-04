
dmesg可以在控制台打印出时间戳

make xxx_config		

/*
	将ARCH、CPU、BOARD、SOC参数传入。mkconfig将根据参数将include目录下的相应头文件链接好，生成config.h
	然后make，分别调用各子目录下的Makefile生成所有的目标文件和库文件*.a
	最后通过u-boot.lds链接start.o和所有库文件，生成ELF映像文件
	不同格式的映像文件都是调用相应工具由ELF映像直接或者间接生成的。
*/