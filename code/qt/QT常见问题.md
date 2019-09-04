### 1 ###
/home/work/code/project/E7525/code_qt/download-tools/download_v1.0/
	build-download_v1-0-Desktop-Debug/moc_widget.cpp:68: error: undefined reference 
	to `Widget::on_btn_showfiles_clicked()'
		一般清除一下就可以，也碰到过清除解决不了的情况，把文件移除项目重新加入就可以了
		知道了，还要在对应的头文件里面把定义删了就不会报错了

		
	

### 2 ###
c++ class does not name a type

declare class does not name a type
	出现这个编译错误主要有四个可能原因，现总结如下：
	1.引用的类命名空间未包含
	2.引用的类头文件未包含
	3.包含了头文件，或者已经前置声明了，则说明所引用的类名写错。
	4.循环引用头文件
	前置声明要素：
	1.前置声明需要注意以上提到的四点
	2.尽可能的采用前置声明（做到只有包含继承类的头文件）
	3.使用前置声明时，cpp文件中include 头文件次序必须先 包含前置声明的类定义头文件，再包含本类头文件。
	否则会出现如下编译错误.
	(expected constructor, destructor, or type conversion before ‘typedef')





### 3 ###
QObject: Cannot create children for a parent that is in a different thread.                                                                        
(Parent is QSerialPort(0x7ffe97351070), parent's thread is QThread(0x869810), current thread is MyThread(0x7ffe97351058)

/home/work/code/project/E7525/code_qt/download-tools/thread_test/thread-test/mythread.cpp:19: error: return type 'class QPoint' is incomplete
 QPoint MyThread::m_read_point_from_file(void)
                                             ^
											 

											 
											 
											
### 4　###											
编译openGL程序时，出现以下问题：	


Qt5.6.2 

使用Qt5.6.2 编译时， 出现/opt/Qt5.6.2/5.6/gcc_64/include/QtGui/qopengl.h:120: error: GL/gl.h: No such file or directory
解决办法：
　　sudo apt-get install libgl1-mesa-dev libglu1-mesa-dev 

										 
:-1: error: cannot find -lGL
网上找了一下很多人都出现了这个错误。 
有两种原因:
	1.版本1(未实测)
	一种是没有按照libGL库，那么就安装：
	sudo apt-get install libgl1-mesa-dev

	1.版本2(实测能解决)
	执行
	sudo apt-get install mesa-common-dev
	编译出现如下错误提示：
	/usr/bin/ld: cannot find -lGL
	执行下面命令解决：
	sudo apt-get install libgl1-mesa-dev libglu1-mesa-dev

	2.
	还有一种是装了，但是路径不对，那么就配置一下路径
	(这种情况一般是自带的有，但是路径不对)：

	$ locate libGL
	/usr/lib/i386-linux-gnu/mesa/libGL.so.1
	/usr/lib/i386-linux-gnu/mesa/libGL.so.1.2.0
	/usr/lib/x86_64-linux-gnu/libGLEW.so.1.10
	/usr/lib/x86_64-linux-gnu/libGLEW.so.1.10.0
	/usr/lib/x86_64-linux-gnu/libGLEWmx.so.1.10
	/usr/lib/x86_64-linux-gnu/libGLEWmx.so.1.10.0
	/usr/lib/x86_64-linux-gnu/libGLU.so.1
	/usr/lib/x86_64-linux-gnu/libGLU.so.1.3.1
	/usr/lib/x86_64-linux-gnu/mesa/libGL.so.1
	/usr/lib/x86_64-linux-gnu/mesa/libGL.so.1.2.0
	/usr/lib/x86_64-linux-gnu/mesa-egl/libGLESv2.so.2
	/usr/lib/x86_64-linux-gnu/mesa-egl/libGLESv2.so.2.0.0
	$ sudo ln -s /usr/lib/x86_64-linux-gnu/mesa/libGL.so.1 /usr/lib/libGL.so
	问题解决

	3.网上其他方法，未实测
	解决方法：
		首先，sudo apt-get install build-essential
		然后尝试"run"，又出现"cannot find -lGL"新错误。
		最后，sudo apt-get install libqt4-dev
		再次尝试"run"，程序成功运行。
		完美解决


### 5 ###
	为什么在MyThread.cpp 中 MyThread m_thread;
						m_thread.start();
					会有报错QThread: Destroyed while thread is still running
而在MyThread.h 中 		MyThread m_thread;
然后在MyThread.cpp中	m_thread.start();
					不会报错。
	
	
	
### 6 ###	
QT中能不能用__FUNCTION__ __LINE__ __FILE__等。
	能用。qDebug() << __FILE__ << __LINE__ << __PRETTY_FUNCTION__;
	建议：
		//Qt-way
		#define MyDBG (qDebug() << __FILE__ << __LINE__ << __PRETTY_FUNCTION__)
		//GCC
		#define MyStdDBG (std::cout << __FILE__ << ":" << __LINE__ << ":" << __PRETTY_FUNCTION__<<std::endl)
		
		


### 7 ###		
/home/work/code/project/E7525/code_qt/download-tools/thread_test/thread-test/m_widget.cpp:25: error: expected primary-expression before ',' token
     connect(&MyThread, SIGNAL(m_send_point(QString)), &m_Widget, SLOT(m_receive_point(QString)));
                      ^					  					 		  
QThread: Destroyed while thread is still running





### 8 ### 
GroupBox里面放按钮，为什么鼠标点击到的是对象是GroupBox，而不是按钮，同时也不能获取到鼠标点击的位置。




### 9 ###
/home/work/code/project/E7525/code_qt/download-tools/download_v1.1/download_v1-1/ui_widget.h:13: error: QtWidgets/QAction: No such file or directory
 #include <QtWidgets/QAction>
                             ^
							 
							 
### 10 ###							 
listwidget行item怎样增宽、加粗




### 11 ###
:-1: error: No rule to make target `../download_v1-1/ui_widget.h', needed by `widget.o'.  Stop.
	一般情况下是makefile文件出了问题. 一般出的问题是由于你的bbb 需要用到你的aaa， 
	而makefile中你的aaa的路径是错误的。 把aaa的路径修改为正确的路径就OK了。
	
	
	
	
### 12 ###
将UI控件删除后，对应的槽函数也删除了，但是出现这种错误。怎样解决。（switch语句里面的case也对应注释了。）	
moc_mywidget.o: In function `myWidget::qt_static_metacall(QObject*, QMetaObject::Call, int, void**)':
moc_mywidget.cpp:(.text+0x81): undefined reference to `myWidget::on_btn_test2_clicked()'
moc_mywidget.cpp:(.text+0xd1): undefined reference to `myWidget::on_btn_sendevent_clicked()'
moc_mywidget.cpp:(.text+0xd9): undefined reference to `myWidget::on_btn_test1_clicked()'
	一般情况是槽函数定义，实现，等相关内容也要清除。重新构建。
	





### 13 ###
getvideothread.o: In function `GetVideoThread::v4lCaptureStart(int)':
/home/work/code/project/E7525/code_qt/ui_e0800/apaUI/build/../ui/videoCode/getvideothread.cpp:144: undefined reference to `GetVideoThread::sigGetBuffAddr(unsigned char*)'
collect2: error: ld returned 1 exit status
make: *** [ui] Error 1
cp: cannot stat ‘ui’: No such file or
	这个问题是自定义类使用了信号与槽，所以要在类定义的时候加入一个宏：
		添加了Q_OBJECT宏
