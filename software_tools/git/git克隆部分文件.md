
项目太大或者只需要一部分内容时使用：
注：稀疏克隆模式第一次设置后，后续无法被关闭
但是可以添加想要克隆的文件或目录，这个需要在
已经克隆的内容被改变的情况下才能生效

具体步骤：
```
//1.指定远程仓库
//2.指定克隆模式: 稀疏克隆模式
//3.指定克隆的文件夹(或者文件)
//4.拉取远程文件
 
git remote add -f origin <url>
git config core.sparsecheckout true
echo “resource/css” >> .git/info/sparse-checkout #resource/css路径
git pull origin master
```

完整例子：
```
mkdir gitSparse
cd gitSparse/
git init
git remote add -f origin https://github.com/bestswifter/MySampleCode.git
ls
git config core.sparsecheckout true
echo "CornerRadius" >> .git/info/sparse-checkout
cat ./.git/info/sparse-checkout 
git pull origin  master 
```