1、直接写颜色值
	在样式表中写入：
	QPushButton
	{
		font-family:Microsoft Yahei;		//设置字体，可选
		color:white;						//设置文字颜色
		background-color:rgb(14, 150, 254);	//设置背景颜色
		border: 1px solid rgb(11,  137, 234);
	}

	QPushButton:hover
	{
		color:white;
		background-color:rgb(44, 137, 255);
		border: 1px solid rgb(11, 137, 234);
	}


	QPushButton:pressed
	{
		color: white;
		background-color: rgb(14, 135, 228);
		border: 1px solid rgb(12, 138, 235);
		padding-left: 3px;
		padding-top: 3px;
	}
表示按钮初始、悬停、按下的状态要显示样子。

	//设置按钮无焦点框，有焦点框很难看
	QPushButton：focus
	{
		outline: none;
	}
	//如果在widget中设置，则所有继承的控件都没有焦点框
	QWidget:focus
	{
		outline: none;
	}
	//其他属性同理 可以这样设置，例如背景颜色


2、在样式表中设置背景图片
	QPushButton
	{
		border-image:url(:/Resources/registeraccount.png);
	}
	
	QPushButton:hover
	{
		border-image:url(:/Resources/registeraccount_hover.png);
	}
	
	QPushButton:pressed
	{
		border-image:url(:/Resources/registeraccount_pressed.png);
	}
	其中，图片位置为资源中的图片。
	能否直接写一个绝对路径的图片未知，理论上是可以的。
	
	
3、在代码中写控件的样式表
	    /*样式表设置,可以设置按钮背景,悬停背景,和按下背景*/
    ui->btn_f->setStyleSheet("QPushButton{border-image: url(../pic/front_up.png);}"
                             "QPushButton:hover{border-image: url(../pic/rear_up.png);}"
                             "QPushButton:checked{border-image: url(../pic/front_down.png);}");
	其他属性的写法类似。
	
	//在代码中设置按钮无聚焦，避免出现无边框
	ui->btn_homepage_release->setFocusPolicy(Qt::NoFocus);
	
	
	
	以按钮为例：
		从外到内，一个按钮包括的东西有：
			margin(外边距)
			border(边框)
			padding(内边距)
			element(元素)
		通常所说的background指的是padding框以内的内容
			写法：
				QPushButton
				{
					border: 10px solid;
					border-color: black;
					padding: 30px;
					background-color: red;
				}