
## 编译API
### PCAN-Basic_Linux-4.3.1
```
cd libpcanbasic/pcanbasic
make clean
make
```
报错
```
Unable to build pcanbasic for Linux: install the pcan driver first
```

## 编译驱动
```
$ cd peak-linux-driver-8.8.0
$ make clean
$ make
```
报错
```
src/pcan-settings.c:53:18: fatal error: popt.h: No such file or directory 
```
解决：
```
sudo apt-get install libpopt-dev
```


## 调用API编写上位机


## 其他命令
    从官网copy的
1. 如果仅仅是使用其设备，使用以下命令就可以查看是否有驱动支持
```
Check: Are CAN drivers part of your Linux environment?

Open a terminal and type:
grep PEAK_ /boot/config-`uname -r`

All PEAK drivers are listed (y = included in kernel, m = separate module) but this may not work in every Linux environment.

Check: Is the CAN device initialized?

Open a terminal and type: lsmod | grep ^peak

If, for example, a USB-based CAN interface from PEAK is connected and initialized, the output will be at least one line starting with peak_usb.
```
2. 如果是做其他用途，比如说上位机开发，则需要下载驱动并安装