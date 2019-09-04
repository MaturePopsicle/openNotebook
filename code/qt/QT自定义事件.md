
/******************************************************************
 *	方式1，在一个按钮事件中，发送自定义事件，来模拟点击另一个按钮
 ******************************************************************/
#if 1
    /*同步方式发送事件:sendevent*/
    QPoint pos(0, 0);
    QMouseEvent event0(QEvent::MouseButtonPress, pos, Qt::LeftButton, Qt::LeftButton, Qt::NoModifier);
    QApplication::sendEvent(ui->btn_move1, &event0);

    QMouseEvent event1(QEvent::MouseButtonRelease, pos, Qt::LeftButton, Qt::LeftButton, Qt::NoModifier);
    QApplication::sendEvent(ui->btn_move1, &event1);
#endif

#if 0
    /*异步方式发送事件:postevent*/
    QMouseEvent *press = new QMouseEvent(QEvent::MouseButtonPress, QPoint(0, 0), Qt::LeftButton, Qt::LeftButton, Qt::NoModifier);
    QApplication::postEvent(ui->btn_move1, press);

    QMouseEvent *release = new QMouseEvent(QEvent::MouseButtonRelease, QPoint(0, 0), Qt::LeftButton, Qt::LeftButton, Qt::NoModifier);
    QApplication::postEvent(ui->btn_move1, release);
#endif

其中event0模拟鼠标按下事件
	event1模拟鼠标松开事件
其中sendEvent是同步发送事件
	postEvent是异步发送事件
其中QPoint pos(0, 0)  和 QPoint(0, 0)的作用是一样的。只不过是两种形式而已。
QMouseEvent::QMouseEvent ( Type type, const QPoint & position, 	
							Qt::MouseButton button, Qt::MouseButtons 
							buttons, Qt::KeyboardModifiers modifiers )
    Constructs a mouse event object.
    The type parameter must be one of QEvent::MouseButtonPress, QEvent::MouseButtonRelease, QEvent::MouseButtonDblClick, or QEvent::MouseMove.
    The position is the mouse cursor's position relative to the receiving widget. The button that caused the event is given as a value from the Qt::MouseButton enum. If the event type is MouseMove, the appropriate button for this event is Qt::NoButton. The mouse and keyboard states at the time of the event are specified by buttons and modifiers.
    The globalPos() is initialized to QCursor::pos(), which may not be appropriate. Use the other constructor to specify the global position explicitly.




/********************************************************
 *  发送界面上设置的点,检查能否在对应位置产生鼠标事件
 ********************************************************/
void Widget::on_btn_sendevent_clicked()
{
    //int x = ui->lineEdit_x->text().toInt();		//界面上手动设置的x轴坐标
    //int y = ui->lineEdit_y->text().toInt();		//界面上手动设置的y轴坐标
    int x = ui->lineEdit_mouse_x->text().toInt();	//界面上手动设置的x轴坐标
    int y = ui->lineEdit_mouse_y->text().toInt();	//界面上手动设置的y轴坐标

    //qDebug() << "send click pos : " << QString::number(x) << "," << QString::number(y);
    QMessageBox::about(this,"sendClickPos","POS:"+ QString::number(x)+" "+QString::number(y));
    
	/*
     *  QWidget* w = QApplication::widgetAt(x, y);
     *      @x : 手动输入的点的x轴坐标
     *      @y : 手动输入的点的y轴坐标
     *      @返回值 : 如果该点有控件,则返回控件的全局位置坐标
     *              如果该点没有控件,则返回0;
     */
    QWidget* w = QApplication::widgetAt(x, y);

    if (w)
    {
        QPoint p = w->mapFromGlobal(QPoint(x,y));		//点的坐标转换
        //QPoint p = w->mapFromParent(QPoint(x, y));
        //qDebug() << "sendevent clicked :" + QString::number(p.x()) + QString::number(p.y());
        qDebug() << "sendevent clicked :" << p.x() << " , " << p.y();

        QMessageBox::information(this,"pos", "pos" + QString::number(p.x()) + QString::number(p.y()));
        QMessageBox::about(this,"QTWidget","title:" + w->objectName());
        
		/*
		 *	如果手动设置的坐标位置上有控件（这里是个按钮）
		 *	开始自定义事件并发送（自定义的鼠标按下和弹起）
		 */
		QMouseEvent* press=new QMouseEvent(QEvent::MouseButtonPress,
                                           p, Qt::LeftButton,Qt::LeftButton,Qt::NoModifier);
        QApplication::postEvent(w,press);
        QMouseEvent* release=new QMouseEvent(QEvent::MouseButtonRelease,
                                           p, Qt::LeftButton,Qt::LeftButton,Qt::NoModifier);
        QApplication::postEvent(w,release);
    }
    else
    {
        QMessageBox::about(this,"QETWidget", "=NULL");
        //qDebug() << "there is no thing . NULL . . .";
    }

}