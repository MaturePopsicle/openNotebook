
1、在终端中直接输入  sudo apt-get install subversion，选择安装即可

2、查看版本命令 svnserve --version（更多命令直接键入svnserve --help可查看到）

3、查看svnserver是否已启动： netstat -ntlp，可看到svn对应的端口3690（如果没有看见，则证明服务未启动，可使用svnserve -d启动svn服务，还可以通过svnserve -d -r /home/wwwwfw/mobile来指定启动目录）

4、建立项目：svnadmin create mobile(mobile为项目名称，位置在当前登录用户的主目录下，如我使用wwwwfw登录，则路径为/home/wwwwfw/mobile）

5、在mobile文件夹中可以看到conf文件夹，可针对conf文件夹中的authz、passwd、svnserve.conf进行设置，svnserve.conf主要设置整体的安全策略，passwd则设置用户名和密码，authz则是设置具体的用户有什么权限。

7、常用svn命令：
	checkout(co)命令：
		svn co url --username user --password password
        根据提示可以输入yes来保存帐号和密码；
		例如：	
			svn checkout https://168.8.80.151/svn/E7525_SGMW_CN210S_HD2DAVM_A1/05_software_development/0513_software_code
			然后输入svn的用户名和密码
	update(up)命令：
        进入到需要更新的目录，输入：svn up；
	commit(ci)命令：
        进入需要提交的目录，输入：svn ci -m "修改信息"
    add命令：
        进入需要提交的目录，输入：svn add filename or path
		添加完之后需要用commit命令提交。
		例如：
			svn add pic/*	//将pic文件夹下的所有文件都加入版本管理
			svn commit -m "备注信息"	//提交刚加入的文件，然后加入备注信息
		

	另外，在vi中也可以不退出编辑的文件来提交文件，

    使用shell命令：:! svn ci -m "commit information.."

===========安装=============================================================
更多详细安装步骤见：ubuntu下svn服务器安装
ubuntu下SVN服务器安装配置 
一、SVN安装
1.安装包
$ sudo apt-get install subversion


2.添加svn管理用户及subversion组
$ sudo adduser svnuser
$ sudo addgroup subversion
$ sudo addgroup svnuser subversion


3.创建项目目录
$ sudo mkdir /home/svn
$ cd /home/svn
$ sudo mkdir fitness
$ sudo chown -R root:subversion fitness
$ sudo chmod -R g+rws fitness


4.创建SVN文件仓库
$ sudo svnadmin create /home/svn/fitness


5.访问方式及项目导入：
$ svn co file:///home/svn/fitness
或者
$ svn co file://localhost/home/svn/fitness
* 注意：
如果您并不确定主机的名称，您必须使用三个斜杠(///)，而如果您指定了主机的名称，则您必须使用两个斜杠(//).
//--
下面的命令用于将项目导入到SVN 文件仓库：
$ svn import -m "New import" /home/svn/fitness file:///home/svnuser/src/fitness
一定要注明导入信息


//--------------------------//
6.访问权限设置
修改 /home/svn/fitness目录下：
svnserve.conf 、passwd 、authz三个文件,行最前端不允许有空格
//--
编辑svnserve.conf文件,把如下两行取消注释
password-db = password
authz-db = authz 


//补充说明
# [general]
anon-access = read
auth-access = write
password-db = passwd
其中 anon-access 和 auth-access 分别为匿名和有权限用户的权限，默认给匿名用户只读的权限,但如果想拒绝匿


名用户的访问，只需把 read 改成 none 就能达到目的。


//--
编辑/home/svnuser/etc/passwd 如下:
[users]
mirze = 123456
test1 = 123456
test2 = 123456
//--
编辑/home/svnuser/etc/authz如下
[groups]
admin = mirze,test1
test = test2
[/]
@admin=rw
*=r
这里设置了三个用户mirze,test1,test2密码都是123456
其中mirze和test1属于admin组，有读和写的权限,test2属于test组只有读的权限


7.启动SVN服务
svnserve -d -r /home/svn
描述说明：
-d 表示svnserver以"守护"进程模式运行
-r 指定文件系统的根位置（版本库的根目录），这样客户端不用输入全路径，就可以访问版本库
如: svn://192.168.12.118/fitness


这时SVN安装就完成了.
局域网访问方式：
例如：svn checkout svn://192.168.12.118/fitness --username mirze --password 123456 /var/www/fitness








ubuntu14.04下svn版本管理系统的安装及常用命令的使用整理
ubuntu14.04下安装svn
$sudo apt-get install subversion 
执行这一步就安装完成了，在ubuntu先安装很方便

安装完成后，创建版本库目录，由于是本地环境，就在某个目录下建立一个目录，如果是真实环境，就是相当于服务器上的目录，由于本地，则就模拟出一个服务器上的一个版本库

$sudo mkdir -p /opt/subverdion/svn ###创建版本库目录
$sudo svnadmin create /opt/subversion/svn ###创建版本库，生成配置文件

配置svn，配置文件都在/opt/subversion/svn

1).首先配置用户
$sudo vim /opt/subversion/svn/conf/passwd 

添加格式：用户名 = 密码
如：xc = xc123

2).配置权限和分组

$sudo vim /opt/subversion/svn/conf/authz

[groups]    ###分配组，行首不能有空格
team1 = zhangsan,lisi   ###在组1中有zhangsan和lisi
team2 = wangwu            ###在组2中只有wangwu

[svn:/]        ###分配权限，
zhangsan = rw
@team1 = rw     ###在组名前需要加上@符号，在用户前不需要加@符号，在team1组中的成员有’读写’的权限
@team2 = r        ###在team2组中的成员有'读'的权限
* =             ###其他用户没有任何权限

3).配置/opt/subversion/svn/conf目录下的 svnserve.conf文件，去掉注释
$sudo vim /opt/subversion/svn/conf

anon-access = none        ###将以前的read改成none
auth-access = write
password-db = passwd    ###
authz-db = authz

4).开启svn服务

$sudo svnserve -d -r /opt/subversion
    -d:指定程序后台运行
    -r:指定svn的服务目录，即版本库的目录
    --listen-port 端口 ：设置端口，默认为3690

 

解决svnserve: Can&#39;t bind server socket: Address already in use
# svnserve -d -r /mnt/westos --listen-port 3691

 


5).验证是否开启成功
$ sudo netstat -anp | grep svnserve
返回以下信息
tcp        0      0 0.0.0.0:3690            0.0.0.0:*               LISTEN      18253/svnserve  

6).如何关闭svnserve
$sudo pstree | grep svn        #查看

$sudo killall svnserve        #关闭


##############
上面六步相当于在服务器上的设置
完成之后，进行如下操作
##############

在家目录下建立一个本地目录（相对与服务器来说）

$mkdir -p workspace/project

$cd /workspace/project

$sudo svn checkout svn://127.0.0.1/svn    #和服务器上建立关联，svn目录是在/opt/subversion/下的svn目录
输入上述命令后，在ubuntu14.04下会弹出一个选项卡，让你填一下密码用户名的东西，自己看着填就可以了

之后在workspace/project目录下

$ll -a 可以看到有一个隐藏文件夹.svn，这个目录下记录的都是用户的各种操作

##############
经过上述的步骤，svn的配置基本完成了，之后就可以进行svn命令操作了

可以sudo update 更新看一下，服务器的文件同步到本地来了没有，可以看到svn目录的出现

**注：在ubuntu下使用svn命令的时候，一般要sudo执行
##############


/****************第一个错误***************************/
xc@wen:~/workspace/project01$ svn add aaa
svn: E155004: 运行“svn cleanup”删除锁 (运行“svn help cleanup”以得到详细信息)
svn: E155004: 工作副本“/home/xc/workspace/project01”已经锁定
svn: E200031: sqlite[S8]: attempt to write a readonly database
svn: E200031: 额外错误:
svn: E200031: sqlite[S8]: attempt to write a readonly database
******************/
出现上面这个时要用root的身份登录才有用，以普通用户会报上面的错误

/****************第二个错误***************************/

当出现svn: E155007: “/opt/subversion”不是工作副本的时候，这个是因为在配置authz权限的时候
[groups]
team1 = xc,lisi
team2 = lisi

[proj01:/] ######在这里冒号和/之间不能有空格
xc = rw

@team1 = rw 
@team2 = r
* = 

 

 

最近经常使用svn进行代码管理，这些命令老是记不住，得经常上网查，终于找了一个linux下svn命令使用大全：

1、将文件checkout到本地目录 
svn checkout path（path是服务器 上的目录）
例如：svn checkout svn://192.168.1.1/pro/domain
简写：svn co

2、往版本库中添加新的文件 
svn add file
例如：svn add test.php(添加test.php)
svn add *.php(添加当前目录下所有的php文件)

3、将改动的文件提交到版本库 
svn commit -m “LogMessage“ [-N] [--no-unlock] PATH(如果选择了保持锁，就使用–no-unlock开关)
例如：svn commit -m “add test file for my test“ test.php
简写：svn ci

4、加锁/解锁 
svn lock -m “LockMessage“ [--force] PATH
例如：svn lock -m “lock test file“ test.php
svn unlock PATH

5、更新到某个版本 
svn update -r m path
例如：
svn update如果后面没有目录，默认将当前目录以及子目录下的所有文件都更新到最新版本 。
svn update -r 200 test.php(将版本库中的文件test.php还原到版本200)
svn update test.php(更新，于版本库同步。如果在提交的时候提示过期的话，是因为冲突，需要先update，修改 文件，然后清除svn resolved，最后再提交commit)
简写：svn up

6、查看文件或者目录状态 
1）svn status path（目录下的文件和子目录的状态，正常状态不显示）
【?：不在svn的控制中；M：内容被修改；C：发生冲突；A：预定加入到版本库；K：被锁定】
2）svn status -v path(显示文件和子目录状态)
第一列保持相同，第二列显示工作版本号，第三和第四列显示最后一次修改的版本号和修改人。
注：svn status、svn diff和 svn revert这三条命令在没有网络的情况下也可以执行的，原因是svn在本地的.svn中保留了本地版本的原始拷贝。
简写：svn st

7、删除 文件 
svn delete path -m “delete test fle“
例如：svn delete svn://192.168.1.1/pro/domain/test.php -m “delete test file”
或者直接svn delete test.php 然后再svn ci -m ‘delete test file‘，推荐使用这种
简写：svn (del, remove, rm)

8、查看日志 
svn log path
例如：svn log test.php 显示这个文件的所有修改记录，及其版本号的变化

9、查看文件详细信息 
svn info path
例如：svn info test.php

10、比较差异 
svn diff path(将修改的文件与基础版本比较)
例如：svn diff test.php
svn diff -r m:n path(对版本m和版本n比较差异)
例如：svn diff -r 200:201 test.php
简写：svn di

11、将两个版本之间的差异合并到当前文件 
svn merge -r m:n path
例如：svn merge -r 200:205 test.php（将版本200与205之间的差异合并到当前文件，但是一般都会产生冲突，需要处理一下）

12、SVN 帮助 
svn help
svn help ci
——————————————————————————

以上是常用命令，下面写几个不经常用的

——————————————————————————

13、版本库下的文件和目录列表 
svn list path
显示path目录下的所有属于版本库的文件和目录
简写：svn ls

14、创建纳入版本控制下的新目录 
svn mkdir: 创建纳入版本控制下的新目录。
用法: 1、mkdir PATH…
2、mkdir URL…
创建版本控制的目录。
1、每一个以工作副本 PATH 指定的目录，都会创建在本地端，并且加入新增
调度，以待下一次的提交。
2、每个以URL指定的目录，都会透过立即提交于仓库中创建。
在这两个情况下，所有的中间目录都必须事先存在。

15、恢复本地修改 
svn revert: 恢复原始未改变的工作副本文件 (恢复大部份的本地修改)。revert:
用法: revert PATH…
注意: 本子命令不会存取网络，并且会解除冲突的状况。但是它不会恢复
被删除的目录


16、代码 库URL变更 
svn switch (sw): 更新工作副本至不同的URL。
用法: 1、switch URL [PATH]
2、switch –relocate FROM TO [PATH...]

1、更新你的工作副本，映射到一个新的URL，其行为跟“svn update”很像，也会将
服务器上文件与本地文件合并。这是将工作副本对应到同一仓库中某个分支或者标记的
方法。
2、改写工作副本的URL元数据，以反映单纯的URL上的改变。当仓库的根URL变动
(比如方案名或是主机名称变动)，但是工作副本仍旧对映到同一仓库的同一目录时使用
这个命令更新工作副本与仓库的对应关系。
我的例子：svn switch --relocate http://59.41.99.254/mytt http://www.mysvn.com/mytt 

17、解决 冲突 
svn resolved: 移除工作副本的目录或文件的“冲突”状态。
用法: resolved PATH…
注意: 本子命令不会依语法来解决冲突或是移除冲突标记；它只是移除冲突的
相关文件，然后让 PATH 可以再次提交。

18、输出指定文件或URL的内容。 
svn cat 目标[@版本]…如果指定了版本，将从指定的版本开始查找。
svn cat -r PREV filename > filename (PREV 是上一版本,也可以写具体版本号,这样输出结果是可以提交的)

19、 查找工作拷贝中的所有遗留的日志文件，删除进程中的锁 。

当Subversion改变你的工作拷贝（或是.svn 中 的任何信息），它会尽可能的小心，在修改任何事情之前，它把意图写到日志文件中去，然后执行log文件中的命令，然后删掉日志文件，这与分类帐的文件系统 架构类似。如果Subversion的操作中断了（举个例子：进程被杀死了，机器死掉了），日志文件会保存在硬盘上，通过重新执行日志文 件，Subversion可以完成上一次开始的操作，你的工作拷贝可以回到一致的状态。

这就是svn cleanup 所作的：它查找工作拷贝中的所有遗留的日志文件，删除进程中的锁。如果Subversion告诉你工作拷贝中的一部分已经“锁定 ”了，你就需要运行这个命令了。同样，svn status 将会使用L 显示锁定的项目：

$ svn status
L somedir
M somedir/foo.c 

$ svn cleanup
$ svn status
M somedir/foo.c

20、 拷贝用户的一个未被版本化的目录树到版本库。
svn import 命令是拷贝用户的一个未被版本化的目录树到版本库最快的方法，如果需要，它也要建立一些中介文件。

$ svnadmin create /usr/local/svn/newrepos $ svn import mytree file:///usr/local/svn/newrepos/some/project Adding mytree/foo.c Adding mytree/bar.c Adding mytree/subdir Adding mytree/subdir/quux.h Committed revision 1.

在上一个例子里，将会拷贝目录mytree 到版本库的some/project 下：

$ svn list file:///usr/local/svn/newrepos/some/project bar.c foo.c subdir/

注意，在导入之后，原来的目录树并没有 转化成工作拷贝，为了开始工作，你还是需要运行svn checkout 导出一个工作拷贝。

另附：为SVN 加入Email通知 
可以通过Subversion的Hook脚本的方式为SVN 加入邮件列表功能 
编译安装了Subversion后 在源码的tools 下有一个comm-email.pl的Perl脚本，在你的档案目录下有一个hooks目录，进入到hooks目录把post-commit.tmpl 改名为post-commit并给它可执行的权限。 
更改post-commit脚本 把comm-email.pl脚本的决对路径加上，否则 SVN 找不到comm-email.pl 

REPOS="$1" 
REV="$2" 
/usr/local/svn /resp/commit-email.pl "$REPOS" "$REV" email@address1.com email@address2.com 
#log-commit.py --repository "$REPOS" --revision "$REV" 

最后一行是用来记日志的 我不用这个功能 所以注释掉了