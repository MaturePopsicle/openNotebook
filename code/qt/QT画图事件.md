
在paintevent函数里画一张图片，然后显示出来：
QImage m_3image(887, 360, QImage::Format_ARGB32_Premultiplied);	//设置要画图片的属性

paint.begin(&m_3image);				//准备在这张图片上画图
paint.setBrush(Qt::gray);			//设置画刷
paint.drawRect(0, 0, 592, 360);		//画一个矩形
paint.setBrush(Qt::darkCyan);		//设置画刷
paint.drawRect(593, 0, 295, 360);	//画另一个矩形
paint.end();						//结束画图

paint.begin(this);					//准备在界面上画这张图片
paint.drawImage(73, 0, m_3image);	//在界面上将刚才画的图片画出来

//用update()函数可以更新paintevent函数

QPainter painter;

painter.drawPixmap(point, pix);	//从point这个点为原点，画pix这张图
painter.drawText(一个方框， 字体， 要显示的字);这个怎么用