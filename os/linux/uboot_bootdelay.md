首次烧写uboot我们可以在此文件夹下修改uboot的bootdelay“uboot/include/configs/xxxx.h”,其中xxxx代表你单板名称

```
#define CONFIG_BOOTDELAY    1
```
“1”表示uboot启动延时为1s



可以通过以下的uboot命令来进行修改，如下：
```
seten bootdelay 2
saveen
```

如果设置为“0”后呢，如下：
```
seten bootdelay 0
```
这样设置后uboot环境变量区的bootdelay就是0，也就是没有启动延时了，我们也没办法再进去uboot菜单管理界面了,此时你可能会去修改我刚才说的“uboot/include/configs/xxxx.h”这个文件夹里面的“CONFIG_BOOTDELAY”然后重新烧写uboot。但是实测告诉你那是不行的，因为uboot每次启动他都先去读取了flash里面的环境变量，除非里面没任何数据才会来取这个宏的定义，但是我们之前已经把“0”写入环境变量区了，那还有救嘛，当然有！只要不让uboot从环境变量里面取不就行了吗！经过查看uboot源码，发现在源码文件“uboot/common/main.c”中做了如下的判断：
```
#if defined(CONFIG_BOOTDELAY) && (CONFIG_BOOTDELAY >= 0)
    s = getenv ("bootdelay");
    bootdelay = s ? (int)simple_strtol(s, NULL, 10) : CONFIG_BOOTDELAY;
    debug ("### main_loop entered: bootdelay=%d\n\n", bootdelay);
```
这样我们再去修改“uboot/include/configs/xxxx.h”下的 CONFIG_BOOTDELAY 这个宏就可以了，把他改为 1 就是延时 1 秒，改为 0 就每次启动都没有延时，这样也符合我们的产品需求。但一般是最后阶段我们才做这个修改，因为这里一旦修改后你通过uboot命令行就无法通过“seten bootdelay”来修改启动延时了，因为它每次都取的是你源码中设置的值。