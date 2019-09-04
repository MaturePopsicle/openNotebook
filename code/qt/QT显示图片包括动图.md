
1、显示动图

QMovie *movie = new QMovie("图片路径+图片名.gif");
ui->label->setMovie(movie);
movie->start();

2、在label上显示图片
QImage *image = new QImage("./pic.jpg");
label->setPixmap(QPixmap::fromImage(image));


QPixmap *pixmap = new QPixmap("./pic.png");
label->setPixmap(pixmap);


3、直接画出图片
在重写paintevent函数，在函数中重画
void Widget::paintEvent(QPiantEvent *e)
{
	QPainter painter(this);
	QPixmap pix;
	pix.load("./../pic.png");
	
	painter.drawPixmap(0, 0, 100, 33, pix);
}


4、在按钮上显示图片，用样式表
ui->btn_f->setStyleSheet("QPushButton{border-image: url(../pic/front_up.png);}");

label类似
ui->label_4->setStyleSheet("QLabel{border-image: url(../pic/limit10.png);}");
