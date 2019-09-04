1、读取目录里面所有文件名
    QDir dir("/home/work/tftp/");		/*指定目录的绝对路径*/
    QStringList infolist = dir.entryList(QDir::NoDotAndDotDot | QDir::AllEntries);	/*获取所有文件名*/

    for(int i=0; i<infolist.size(); i++)
    {
        if(0 == i)
        {
            qDebug() << infolist.size() ;		/*指定目录下的文件数*/
        }

        ui->listWidget_filenames->addItem(infolist.at(i));
        qDebug() << dir.absolutePath() + "/" + infolist.at(i) ;		/*目录的绝对路径加上文件名，得到文件的绝对路径*/
    }