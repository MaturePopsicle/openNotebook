### 1 ###
/home/work/code/project/E7525/code_qt/download-tools/download_v1.0/
	build-download_v1-0-Desktop-Debug/moc_widget.cpp:68: error: undefined reference 
	to `Widget::on_btn_showfiles_clicked()'
		һ�����һ�¾Ϳ��ԣ�Ҳ���������������˵���������ļ��Ƴ���Ŀ���¼���Ϳ�����
		֪���ˣ���Ҫ�ڶ�Ӧ��ͷ�ļ�����Ѷ���ɾ�˾Ͳ��ᱨ����

		
	

### 2 ###
c++ class does not name a type

declare class does not name a type
	����������������Ҫ���ĸ�����ԭ�����ܽ����£�
	1.���õ��������ռ�δ����
	2.���õ���ͷ�ļ�δ����
	3.������ͷ�ļ��������Ѿ�ǰ�������ˣ���˵�������õ�����д��
	4.ѭ������ͷ�ļ�
	ǰ������Ҫ�أ�
	1.ǰ��������Ҫע�������ᵽ���ĵ�
	2.�����ܵĲ���ǰ������������ֻ�а����̳����ͷ�ļ���
	3.ʹ��ǰ������ʱ��cpp�ļ���include ͷ�ļ���������� ����ǰ���������ඨ��ͷ�ļ����ٰ�������ͷ�ļ���
	�����������±������.
	(expected constructor, destructor, or type conversion before ��typedef')





### 3 ###
QObject: Cannot create children for a parent that is in a different thread.                                                                        
(Parent is QSerialPort(0x7ffe97351070), parent's thread is QThread(0x869810), current thread is MyThread(0x7ffe97351058)

/home/work/code/project/E7525/code_qt/download-tools/thread_test/thread-test/mythread.cpp:19: error: return type 'class QPoint' is incomplete
 QPoint MyThread::m_read_point_from_file(void)
                                             ^
											 

											 
											 
											
### 4��###											
����openGL����ʱ�������������⣺	


Qt5.6.2 

ʹ��Qt5.6.2 ����ʱ�� ����/opt/Qt5.6.2/5.6/gcc_64/include/QtGui/qopengl.h:120: error: GL/gl.h: No such file or directory
����취��
����sudo apt-get install libgl1-mesa-dev libglu1-mesa-dev 

										 
:-1: error: cannot find -lGL
��������һ�ºܶ��˶�������������� 
������ԭ��:
	1.�汾1(δʵ��)
	һ����û�а���libGL�⣬��ô�Ͱ�װ��
	sudo apt-get install libgl1-mesa-dev

	1.�汾2(ʵ���ܽ��)
	ִ��
	sudo apt-get install mesa-common-dev
	����������´�����ʾ��
	/usr/bin/ld: cannot find -lGL
	ִ��������������
	sudo apt-get install libgl1-mesa-dev libglu1-mesa-dev

	2.
	����һ����װ�ˣ�����·�����ԣ���ô������һ��·��
	(�������һ�����Դ����У�����·������)��

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
	������

	3.��������������δʵ��
	���������
		���ȣ�sudo apt-get install build-essential
		Ȼ����"run"���ֳ���"cannot find -lGL"�´���
		���sudo apt-get install libqt4-dev
		�ٴγ���"run"������ɹ����С�
		�������


### 5 ###
	Ϊʲô��MyThread.cpp �� MyThread m_thread;
						m_thread.start();
					���б���QThread: Destroyed while thread is still running
����MyThread.h �� 		MyThread m_thread;
Ȼ����MyThread.cpp��	m_thread.start();
					���ᱨ��
	
	
	
### 6 ###	
QT���ܲ�����__FUNCTION__ __LINE__ __FILE__�ȡ�
	���á�qDebug() << __FILE__ << __LINE__ << __PRETTY_FUNCTION__;
	���飺
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
GroupBox����Ű�ť��Ϊʲô����������Ƕ�����GroupBox�������ǰ�ť��ͬʱҲ���ܻ�ȡ���������λ�á�




### 9 ###
/home/work/code/project/E7525/code_qt/download-tools/download_v1.1/download_v1-1/ui_widget.h:13: error: QtWidgets/QAction: No such file or directory
 #include <QtWidgets/QAction>
                             ^
							 
							 
### 10 ###							 
listwidget��item���������Ӵ�




### 11 ###
:-1: error: No rule to make target `../download_v1-1/ui_widget.h', needed by `widget.o'.  Stop.
	һ���������makefile�ļ���������. һ������������������bbb ��Ҫ�õ����aaa�� 
	��makefile�����aaa��·���Ǵ���ġ� ��aaa��·���޸�Ϊ��ȷ��·����OK�ˡ�
	
	
	
	
### 12 ###
��UI�ؼ�ɾ���󣬶�Ӧ�Ĳۺ���Ҳɾ���ˣ����ǳ������ִ��������������switch��������caseҲ��Ӧע���ˡ���	
moc_mywidget.o: In function `myWidget::qt_static_metacall(QObject*, QMetaObject::Call, int, void**)':
moc_mywidget.cpp:(.text+0x81): undefined reference to `myWidget::on_btn_test2_clicked()'
moc_mywidget.cpp:(.text+0xd1): undefined reference to `myWidget::on_btn_sendevent_clicked()'
moc_mywidget.cpp:(.text+0xd9): undefined reference to `myWidget::on_btn_test1_clicked()'
	һ������ǲۺ������壬ʵ�֣����������ҲҪ��������¹�����
	





### 13 ###
getvideothread.o: In function `GetVideoThread::v4lCaptureStart(int)':
/home/work/code/project/E7525/code_qt/ui_e0800/apaUI/build/../ui/videoCode/getvideothread.cpp:144: undefined reference to `GetVideoThread::sigGetBuffAddr(unsigned char*)'
collect2: error: ld returned 1 exit status
make: *** [ui] Error 1
cp: cannot stat ��ui��: No such file or
	����������Զ�����ʹ�����ź���ۣ�����Ҫ���ඨ���ʱ�����һ���꣺
		�����Q_OBJECT��
