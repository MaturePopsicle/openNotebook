


代码布局基本：
	水平布局 QHBoxLayout	
	垂直布局 QVBoxLayout
		QWidget *window = new QWidget;
		QPushButton *button1 = new QPushButton("One");
		QPushButton *button2 = new QPushButton("Two");
		QPushButton *button3 = new QPushButton("Three");
		QPushButton *button4 = new QPushButton("Four");
		QPushButton *button5 = new QPushButton("Five");

		QHBoxLayout *layout = new QHBoxLayout;
		layout->addWidget(button1);
		layout->addWidget(button2);
		layout->addWidget(button3);
		layout->addWidget(button4);
		layout->addWidget(button5);

		window->setLayout(layout);
		window->show();
	
	表格布局 QFormLayout 
		QWidget *window = new QWidget;
		QPushButton *button1 = new QPushButton("One");
		QLineEdit *lineEdit1 = new QLineEdit();
		QPushButton *button2 = new QPushButton("Two");
		QLineEdit *lineEdit2 = new QLineEdit();
		QPushButton *button3 = new QPushButton("Three");
		QLineEdit *lineEdit3 = new QLineEdit();

		QFormLayout *layout = new QFormLayout;
		layout->addRow(button1, lineEdit1);
		layout->addRow(button2, lineEdit2);
		layout->addRow(button3, lineEdit3);

		window->setLayout(layout);
		window->show();
	
	栅格布局 QGridLayout
		QWidget *window = new QWidget;
		QPushButton *button1 = new QPushButton("One");
		QPushButton *button2 = new QPushButton("Two");
		QPushButton *button3 = new QPushButton("Three");
		QPushButton *button4 = new QPushButton("Four");
		QPushButton *button5 = new QPushButton("Five");

		QGridLayout *layout = new QGridLayout;
		layout->addWidget(button1, 0, 0);
		layout->addWidget(button2, 0, 1);
		layout->addWidget(button3, 1, 0, 1, 2);
		layout->addWidget(button4, 2, 0);
		layout->addWidget(button5, 2, 1);

		window->setLayout(layout);
		window->show();
	