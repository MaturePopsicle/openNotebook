    lineEdit.setFont(QFont("Timers" , 28 ,  QFont::Bold)); 	//可用


    

    lineEdit.setStyleSheet("color:red");//文本颜色  		//可用
    lineEdit.setStyleSheet("background-color:red");//背景色 
	
	
		字体描边，在paintevent中写
	#if 1
		QPainter painter(this);
		QFont font;
		font.setPointSize(50);
		font.setBold(true);

		if(1)	//描边
		{
			QFontMetrics metrics(font);
			QPainterPath path;
			QPen pen(QColor(0, 0, 0, 100));
			int penwideth = font.pointSize() * 0.2;

			if(penwideth > 6)
				penwideth = 6;

			pen.setWidth(penwideth);
			int len = metrics.width("hello world.");
			int w = width();
			int px = (len - w) / 2;
			if(px < 0)
				px = -px;

			int py = (height() - metrics.height()) / 2 + metrics.ascent();
			if(py < 0)
				py = -py;

			path.addText(px, py, font, "hello world.");
			painter.strokePath(path, pen);
			painter.fillPath(path, QBrush(Qt::cyan));

		}
		else
		{
			//不描边，正常drawText.
		}
	#endif
