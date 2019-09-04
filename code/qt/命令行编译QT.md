2.1.在 hello.cpp所在目录下，运行命令：qmake  -project
			/* 生成.pro 文件 */
        hello.cpp 同目录下有hello.pro文件被生成，它是与平台无关的工程文件。
        注：此处因为版本QT4和QT5的原因，需要修改hello.pro文件，
		具体修改内容如下：在.pro文件中加入以下代码：
			QT += widgets core gui
			
2.2. 在 hello.cpp所在目录下，运行命令：qmake hello.pro
			/* 根据.pro文件生成Makefile*/
		同目录下有 Makefile文件被生成（Makefile是指导编译器编译源代码的配置文件，
		在其目录下输入make命令(nmake在win32,vc6环境)就可以完成编译）。
2.3.在 hello.cpp所在目录下，运行命令：make
			/* 生成可执行文件 */
		同目录下有 hello,hello.o两个文件被编译生成。其中 hello就是在当前 
		Linux 系统下使用 Qt编译生成的可执行文件了。