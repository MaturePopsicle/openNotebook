

版本5.5.1

环境配置
/etc/profile
#echo "===== TSH 360 System ====="
# export TSH_DISABLE_3DVIEW=1
export TSH_ENABLE_HANGSHENG_STYLE_TRACK=1
export FB_MULTI_BUFFER=3
export GPU_VIV_DISABLE_CLEAR_FB=1
export QT_QPA_PLATFORM=eglfs
export QT_QPA_EGLFS_FB=/dev/fb1
export QT_QPA_EVDEV_KEYBOARD_PARAMETERS=repeat-delay\=100:repeat-rate\=333
export QT_QPA_GENERIC_PLUGINS=evdevtouch:/dev/input/event0
# export QT_QPA_EGLFS_DISABLE_INPUT=1
# export VPU_LIB_DBG=10