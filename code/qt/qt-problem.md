connect(&my_serial_port, &QSerialPort::readyRead, this, &MyThread::m_serial_data_handle);

其中槽函数m_serial_data_handle要不要设置互斥锁，在执行完之前不允许多次进入


[root@imx6qdlsolo:~]# 
[root@imx6qdlsolo:~]# ./readyTest 
Unable to query physical screen size, defaulting to 100 dpi.
To override, set QT_QPA_EGLFS_PHYSICAL_WIDTH and QT_QPA_EGLFS_PHYSICAL_HEIGHT (in millimeters).


"------21:54:54:335------ pressed.(x, y)" 1608 ,  65
"======21:54:54:335====== receive point."
"======21:54:54:335====== objectName : " "btn_close"
thread stopped.
"++++++21:54:54:536++++++ send done."
"======21:54:54:536====== emit point done ."
QThread: Destroyed while thread is still running
QWaitCondition::wakeAll(): mutex lock failure: Invalid argument



qapplication a(argc, *argv[]);	//这句话是什么作用
MainWindow m;
a.setMainWidget(&m);		//什么意思


