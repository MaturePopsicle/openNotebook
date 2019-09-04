1、QT常用快捷键及命令
	ctrl+/		将选中的代码全都用"//"注释



2、转换
	字符串转double
		a、	QString str = "123.45"
			double val = str.toDouble();	//val=123.45
		转为float类似toFloat
		转为整型也类似toInt
	
	数字转字符串
		a、常整型转为QString
			long a = 63
			QString str = QString::number(a,16);	//str="3f"
			QString str = QString::number(a,16).toUpper();	//str="3F"
		b、数字转换成字符串
			int i = 100
			QString str = QString::number(i)


1、 一种方法是设置它的最大窗口值和最小窗口值，并且使最大值和最小值相等。 
简单的示例： setMinimumSize(370, 150); setMaximumSize(370, 150); 
此时窗口大小便被固定为（370,150）。

2、一种方法是使用setFixedSize()，这样一句话就可以解决问题。 
简单的示例： setFixedSize(365,240); 
窗口的最大化按钮将变得不可用.

后来发现还有一个方法就是  resize。在构造函数中直接调用他设置大小就可以。如：
this->resize( QSize( 800, 600 ));




Constant	Value	Description
Qt::WindowNoState	0x00000000	The window has no state set (in normal state).
Qt::WindowMinimized	0x00000001	The window is minimized (i.e. iconified).
Qt::WindowMaximized	0x00000002	The window is maximized with a frame around it.
Qt::WindowFullScreen	0x00000004	The window fills the entire screen without any frame around it.
Qt::WindowActive	0x00000008	The window is the active window, i.e. it has keyboard focus.
有了这个就非常easy 了，想让窗体最大化，只需要
setWindowState(Qt::WindowMaximized);就行了


Qt全屏显示函数        
1、window.showFullScreen()//此方法只对顶级窗口有效，对子窗口无效
2、yourwidget->setWindowFlags(Qt::window | Qt::FramelessWindowHint); 
   （第一个Qt::window表示此widget是窗口类型，第二个参数使用无框架就是没有标题，状态栏和边框）
Qt最大化显示函数         window.showMaximized()
Qt最小化显示函数         window.showMinimized()
Qt固定尺寸显示函数         window.resize(x,y)




  //设置无边框透明
  setWindowFlags(Qt::FramelessWindowHint);//无边框
  setAttribute(Qt::WA_TranslucentBackground);//背景透明




pushButton->setGeometry(10,10,200,200); //前两个参数是位置坐标，后两个参数是按钮的尺寸。 

 