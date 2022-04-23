# Linux介绍

## Linux是什么, 能干什么?

### 简介

根据Wikipedia, Linux是一系列基于Linux内核的操作系统. 
而Linux内核是由大名鼎鼎的Linus Torvalds开发.

### Linux有什么用途

Linux最常见的用途是服务器. 相当一部分网站或其他网络服务的服务器都是Linux.
一方面原因是Linux是免费的, 另一方面Linux服务器的运维相比Windows Server其实更加简单, 也更加广泛.
学会Linux可以使我们可以进行一些运维工作.

由于Windows的受众是几乎所有使用电脑的人, 其各种设计都更加面向大众群体使用, 所以在日常使用中完全可以
不接触一些计算机技术细节. Linux则相反, 在使用过程中会发现各种各样计算机技术的体现, 
例如文件重定向, 正则表达式, 脚本编程, 权限, 配置文件等, 甚至就一个黑底白字的命令行都吓跑了不少人
(所以说不要怕, 命令行并不是难, 只是需要时间适应).
在Linux学习过程中, 其实可以学到很多非常有用的计算机知识, 而且往往是学校专业课教不到的.
而当你适应了Linux, 你会发现在偏计算机技术类的事情上, Linux有时要比Windows更易用也强大.
(打游戏和Office之类还是乖乖保留Windows用吧)

Linux也应用于嵌入式, 也就是为设施量身定制操作系统的场景, 如路由器, 自动化控制系统, 智能家居, 智能汽车等.
所以Linux也适合于想从事Linux嵌入式的同学.
(不过感觉学校里身边见的还是蛮少的, 可能需要各位自行去探索)

### Linux简史

UNIX诞生于贝尔实验室, 是一个多任务多用户操作系统, 在当时那个年代相当先进.
在1970年代, AT&T将UNIX向外界授权后, 出现了各种各样类UNIX操作系统, 如BSD, Solaris, 和Minix.

Minix是由Andrew S. Tanenbaum开发的用于学术的类UNIX.
Linus Torvalds在大学时, 非常喜欢Minix. 但随后他发现Minix有许多可改进之处, 便向Minix的作者Andrew发邮件提修改建议.
结果对方并不认同Linus提出的很多观点. 于是Linus就着手打造一个Minix的改进版.
他根据POSIX规范(一个UNIX操作系统接口规范), 自己写代码完成了一个全新的类UNIX系统.

Linus起初想给这个新系统命名"free", "freak"和"x"一类的名字, 认为"Linux"这个名字有点自大(Linux = Linus'UNIX). 
但是当时Linux开发的FTP服务器的志愿管理员没通知Linus就擅自给项目命名"Linux", Linus之后也同意使用这个名字.
Linux这个名字便由此而来.

Linux一经发布便受到了四海八方开发者的喜爱. 如今的Linux内核开发是由世界各地的开发者贡献对代码的修改, 
再统一筛选合并. 这种便是开源软件的开发模式.
如今运行的绝大部分类UNIX操作系统都是Linux.


## Linux命令行使用简介

Linux的特色与强项都在命令行. 相比与Windows的命令提示符或PowerShell, Linux命令行, 也就是shell, 无疑更加易用且强大.
(听说PowerShell也蛮强的, 但是感觉会用的人不多)

### 文件操作

不管是什么操作系统, 文件操作都是都是非常基本的操作.

- ls	- list			显示目录的文件内容
- cd	- change directory	改变当前目录
- mkdir	- make directory	新建目录

Linux的文件系统是组织成树状结构的.

相对路径和绝对路径. 相对路径取决于当前所在路径.

```bash
ls
mkdir first-dir
cd first-dir
ls
cd ..
ls
```

其他命令

- touch	- touch			新建或更新一个文件的时间戳
- cp	- copy			复制文件或目录
- mv	- move			移动文件或目录
- rm	- remove		删除文件或目录
- cat	- concatenate		显示文件内容



```bash
cd first-dir
touch first-file
cp first-file second
mv second second-file
cp ../.bashrc ./bashrc
cat bashrc
rm bashrc
```

### man

```bash
cd first-dir
mkdir another-dir
rm another-dir
```

是否发现删不掉.

这个时候我们可以去查询rm的手册, 通过man命令, 而且不需要联网.

```bash
man rm
```

man页面介绍.

内容很多, 想要快速查找? 使用正则查找.

按下"/", 输入"directory", 回车, 会看到匹配到了"directory".

看描述, 知道需要参数"-r".

"q"退出.

```bash
rm -r another-dir
```

成功.

掌握man命令的使用十分重要. Linux很多命令在初期并不容易记住, 
man无疑是你的小帮手.

### 包管理

没有软件也不知道如何安装软件? 解法是包管理.

包管理需要root权限, 所以需要前缀sudo.

sudo apt-get install nano gcc

输入"y"并回车.

就开始了安装.

```bash
man apt-get
```

### 在Linux中编写运行C程序

```bash
nano hello.c
```

```c
#include <stdio.h>

int main() {
	printf("hello linux\n");
	return 0;
}
```

^X保存退出.

```bash
ls
gcc -o hello hello.c
./hello
```

你就成功地编译并运行了一个C程序.

### 编写Bash脚本

还可以通过脚本自动化这个过程.

```bash
nano compile.sh
```

```bash
#!/bin/bash
gcc -o $1 $1.cpp
./$1
```

保存.

```bash
chmod +x compile.sh
rm hello
ls
./compile.sh hello
```

这个脚本就帮你完成了编译和运行.

### 尝试在你的Linux上运行一个web服务器

```bash
sudo apt-get install nginx
sudo systemctl start nginx
```

然后在浏览器地址栏输入http://HOSTNAME

wsl就是http://localhost

虚拟机就在里面开浏览器http://localhost

云服务器还需要在控制台打开80端口的权限, 然后访问http://HOSTNAME
