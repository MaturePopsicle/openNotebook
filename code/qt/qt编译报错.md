getvideothread.o: In function `GetVideoThread::v4lCaptureStart(int)':
/home/work/code/project/E7525/code_qt/ui_e0800/apaUI/build/../ui/videoCode/getvideothread.cpp:144: undefined reference to `GetVideoThread::sigGetBuffAddr(unsigned char*)'
collect2: error: ld returned 1 exit status
make: *** [ui] Error 1
cp: cannot stat ‘ui’: No such file or


添加了Q_OBJECT宏