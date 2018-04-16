# 在成长的过程中遇到的一些小技巧
## linux
> linux下的一些命令也可以用在git中，现在将一些常用的做一个整理
1. 创建文件：```vi README.md```or ```touch README.md```,创建文件夹： ```mkdir tip```
2. ```ls```查看当前文件夹下面的东西，```cd /```进入某个文件夹，```cd ..```回到上级目录，```cd -```回到上次打开的目录，```pwd```print working directory，打印当前路径
3. ```rm -r 文件夹```删除文件夹及下面的文件，如：```rm -r ./a.md/```
4. ```mv ../gitTip.md .```将上级目录的gitTip.md 移动到当前文件夹下
5. ```cp gitTip.md ../```将当前目录下的gitTip.md复制到上级目录下去
6. ```find . -name "*.md"```查找当前目录及下面的子文件夹里面后缀为md的文件和文件夹
## windows
+ DOS下```cls```清屏
+ ```netstat -ano```查看端口使用情况，```netstat -ano|findstr "80"```查看80端口的使用情况，```tasklist|findstr (pid)```根据查找到的pid找出使用80端口的进程