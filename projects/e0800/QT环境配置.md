

this->setWindowFlags(Qt::Window | Qt::FramelessWindowHint)

export QT_QPA_GENERIC_PLUGINS=evdevtouch:/dev/input/event0

错误的声明:
export QT_QPA_GENERIC_PLUGINS=/dev/input/event0

	

#这个是触摸屏幕的旋转，和颠倒
export QT_QPA_EVDEV_TOUCHSCREEN_PARAMETERS=/dev/input/event0:rotate=180:invertx and inverty 

export QT_QPA_EVDEV_TOUCHSCREEN_PARAMETERS=/dev/input/event0:invertx

export QT_QPA_EVDEV_TOUCHSCREEN_PARAMETERS=/dev/input/event0:rotate=90:invertx and inverty
export QT_QPA_EVDEV_TOUCHSCREEN_PARAMETERS=/dev/input/event0:rotate=180:invertx and inverty
export QT_QPA_EVDEV_TOUCHSCREEN_PARAMETERS=/dev/input/event0:rotate=90
export QT_QPA_EVDEV_TOUCHSCREEN_PARAMETERS=/dev/input/event0:rotate=180
export QT_QPA_EVDEV_TOUCHSCREEN_PARAMETERS=/dev/input/event0:rotate=270
export QT_QPA_EVDEV_TOUCHSCREEN_PARAMETERS=/dev/input/event0:invertx and inverty
export QT_QPA_EVDEV_TOUCHSCREEN_PARAMETERS=/dev/input/event0:inverty

export QT_QPA_EGLFS_WIDTH=1920
export QT_QPA_EGLFS_HEIGHT=720

export QT_QPA_EGLFS_PHYSICAL_WIDTH=1920
export QT_QPA_EGLFS_PHYSICAL_HEIGHT=720
export QT_QPA_EGLFS_DEPTH=16