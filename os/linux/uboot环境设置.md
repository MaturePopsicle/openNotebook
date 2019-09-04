setenv bootfile uImage
setenv root=/dev/mmcblk1p1
...
saveenv
run bootcmd 或者 bootm