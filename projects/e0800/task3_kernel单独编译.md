
## 环境声明
```
export PATH=$PATH:/opt/tools/arago-2016.12/sysroots/x86_64-arago-linux/usr/bin
```



## 使用ti的默认配置生成.config文件
```
make ARCH=arm  CROSS_COMPILE=arm-linux-gnueabihf- ti_sdk_dra7x_release_defconfig
```



## 修改默认配置
```
make ARCH=arm  CROSS_COMPILE=arm-linux-gnueabihf- menuconfig
```
可以添加热插拔，触摸屏，mt7601网卡支持等配置

## 编译设备树
编译之前可以修改配置
```
make ARCH=arm  CROSS_COMPILE=arm-linux-gnueabihf- dra7-evm-infoadas.dtb
```

## 编译内核
```
make ARCH=arm  CROSS_COMPILE=arm-linux-gnueabihf- zImage
```

