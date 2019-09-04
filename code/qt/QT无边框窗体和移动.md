

    m_press = false;
    
	/*这一句中的Qt::FramelessWindowHint是设置无边框窗体，其他都是为了鼠标能够移动窗体*/
	this->setWindowFlags(Qt::Window | Qt::FramelessWindowHint);
    
	/*第二个参数是设置无边框,第三个参数是允许任务栏按钮右键菜单,第四个参数是允许最小化与还原*/
    //this->setWindowFlags(Qt::Window | Qt::FramelessWindowHint | Qt::WindowSystemMenuHint | Qt::WindowMinimizeButtonHint);
   
	
	this->setMouseTracking(true);
	
void Widget::mousePressEvent(QMouseEvent *e)
{
    m_press = true;
    m_start_point = e->pos();
}

void Widget::mouseReleaseEvent(QMouseEvent *e)
{
    m_press = false;
    m_end_point = e->pos();
}

void Widget::mouseMoveEvent(QMouseEvent *e)
{
    if(m_press)
    {
        m_end_point = e->globalPos();
        this->move(m_end_point - m_start_point);
    }
}