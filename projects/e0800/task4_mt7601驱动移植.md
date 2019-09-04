
# 驱动配置修改
## 添加tda2x的配置：
### 添加tda2x交叉编译配置
	在顶层Makefile中添加：
```
//添加
PLATFORM = TDA2X
//注释掉原来的平台
#PLATFORM = IMX6

//添加编译工具路径
# add by Sam 2019-08-03
ifeq ($(PLATFORM),TDA2X)
LINUX_SRC = /home/work/work/e0800/code/apa3.4/ti_components/os_tools/linux/kernel/omap
CROSS_COMPILE = /opt/tools/arago-2016.12/sysroots/x86_64-arago-linux/usr/bin/arm-linux-gnueabihf-
export ARCH=arm
endif
```

### 添加编译配置
	在os/linux/config.mk文件中添加：
```
ifeq ($(PLATFORM),TDA2X)
	EXTRA_CFLAGS := $(WFLAGS) -mfloat-abi=soft -Wno-error=date-time
endif
```

# 内核配置修改
## 添加无线网卡支持
## 重新编译内核


问题3：
/home/work/work/e0800/task_wifi/mt7601u_driver_linux-master/os/linux/../../os/linux/sta_ioctl.c:2380:2: error: unknown field 'private' specified in initializer
  .private = (iw_handler *) rt_priv_handlers,

原因：内核配置不支持802.11的无线设备驱动
解决办法：重新配置内核，支持对应驱动后再次编译


问题2：
/home/work/work/e0800/task_wifi/mt7601u_driver_linux-master/os/linux/../../sta/sta_cfg.c:5766:85: error: macro "__DATE__" might prevent reproducible builds [-Werror=date-time]
             snprintf(extra, size, "Driver version-%s, %s %s\n", STA_DRIVER_VERSION, __DATE__, __TIME__ );
原因：编译参数配置不正确
解决办法：
```
EXTRA_CFLAGS += -Wno-error=date-time       
# Fix compile error on gcc 4.9 and later   不做错误报出
```

问题1：
gnu/stubs-soft.h: No such file or directory
原因：编译参数配置不正确
解决办法：
```
EXTRA_CFLAGS := $(WFLAGS) -mfloat-abi=soft
```




