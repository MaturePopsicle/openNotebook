
设置按钮按下不自动弹起。按下第二次再弹起。
    ui->pushButton->setCheckable(true);
    ui->pushButton->setChecked(true);
	
按钮或者控件设置快捷键：在设置文字时，加上&即可，&后面那个
单词的首字母就是快捷键字母，快捷键操作：Alt+字母 
	ui->radioButton->setText("btn &radio");
	
设置的排他性。autoExclusive(bool)控制按钮是否有排他性。
如果按钮已经放在一个button group中，那么autoExclusive属性将失效
QButtonGroup默认是exclusive（独有的），所以只要它的组内所有按钮都是
checkable(true)的，不管是不是QRadioButton,都将表现的与QRadioButton一样。
如果已经设置了一个exclusive(按钮组默认是的)的按钮组，最好为它设置一个初
选项，否则组内将没有任何一个按钮被选中，这不太符合“one of many”的设计。
具体实现：
	ui->pushButton->setCheckable(true);
    ui->pushButton_2->setCheckable(true);
    ui->pushButton_3->setCheckable(true);
    ui->pushButton_4->setCheckable(true);
    ui->pushButton_5->setCheckable(true);

    buttongroup = new QButtonGroup(this);

    buttongroup->addButton(ui->pushButton, 1);
    buttongroup->addButton(ui->pushButton_2, 2);
    buttongroup->addButton(ui->pushButton_3, 3);
    buttongroup->addButton(ui->pushButton_4, 4);
    buttongroup->addButton(ui->pushButton_5, 5);

	ui->pushButton->setChecked(true);//设置一个按钮被选中。

	//将按钮组信号与自己定义的槽函数相连。根据int型按钮ID判断是组内哪个按钮。
    connect(buttongroup, SIGNAL(buttonClicked(int)), this, SLOT(onButtonJudge(int)));