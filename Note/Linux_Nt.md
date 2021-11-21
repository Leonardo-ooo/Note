Linux Note

**类Unix系统目录结构**

​	一切皆文件

​		

![类Unix系统目录结构](D:\work\Note_git\Note\Picture\类Unix系统目录结构.png)

文件信息：

```
-/xxx/xxx/xxx 1 用户组 时间
首位表示文件类型：
	-：普通文件
	d目录
	l：符号连接文件（软连接）
	b：块文件
	c：为字符设备（键盘、鼠标）
	p：管道设备
	s：本地套接字
后面三个为一组，依次为归属用户的权限，归属组的权限，归属其他用户的权限，r表示可读，w表示可写,x表示可执行，-为无权限，权限位可以写成一个八进制数，四位八进制数0XXX可以表示文件权限，称为权限位数字表示法
数字为硬连接计数
硬连接：使用同一块磁盘区域
软连接：类似于快捷方式
用户家目录下的.bashrc文件加载用户选项
```

**指令意义**

```
用户名@机器名:~/当前目录$
~表示用户家目录，例如：/home/leonardo
$表示当前权限为一般用户，若为管理员，显示#
```



**常用指令**

```
sudo su		//切换到管理员
alias		//自定义指令别名
sudo apt-get install ssh-serve	//安装ssh服务
ctrl + c	//终止
ctrl + z 	//挂起
查看：
    history		//查看历史指令
    ls <目录>	   //查看文件信息， -R 显示文件具体结构
    pwd			//显示当前工作目录
    tree <目录>  //显示文件树
    cat	<文件>	//直接显示文件信息
    more/less 	//查看文件（和cat相似）
    head/tail	//显示头/尾文件内容，默认显示10行， -n参数指定行数。tail的-f参数能实时显示文件尾的变动
	man		//帮助手册
	echo	//显示变量或字符串
	date 	//查看日期 date +"%Y%m%d"
	umask	//查看补码， -s文字显示文件权限
	free	//查看内存占用
	top		//查看CPU占用率
	df		//查看硬盘占用和挂载点
	lsblk	//查看块设备
	netstat 查看端口
		-ant	查看所有被占用端口
	ps		//查看当前终端进程， -ef查看全部系统进程， -xH查看所有线程
		UID    ：启动进程的操作系统用户。
        PID    ：进程编号。
        PPID   ：进程的父进程的编号。
        C      ：CPU使用的资源百分比。
        STIME  ：进程启动时间。
        TTY    ：进程所属的终端。
        TIME   ：使用掉的CPU时间。
        CMD    ：是什么指令。

操作：
    mkdir		//创建目录，支持同时创建多个目录，用空格分隔。-p 递归的创建多个目录
    rmdir <目录>	//删除目录，只能删除空目录，支持同时删除多个目录，用空格分隔。 -p从子目录递归删除空目录
    rm <文件>		//删除文件， -r 删除目录
    which <指令>	//显示对应指令所在位置
    touch <文件名>	//创建文件
    cp <文件> <目录> //拷贝文件到目标目录， -r 递归拷贝<目录1>到<目录2>下。若目录2最小子目录不存在则将	目录1拷贝到该位置并改名为该子目录
    cp <文件1> <文件2>	//拷贝文件1到文件2，若文件2不存在则创建
    mv	//和cp命令基本相同，但mv不保留原文件
    
    ln <文件1> <文件2>	//创建文件2连接到文件1， -s参数创建软连接
    unlink	//删除软硬连接，当硬连接计数为0时删除文件
    ldd 	//查看依赖
    
    chmod	//改变文件权限， u/g/o/a +/- rwx 参数表示用户/组/其他用户/所有 增加/减少 各种权限
    		//数字表示法 + filename
	chown 用户:组 <文件>	//改变文件归属（需要管理员权限）

统计：
    wc	//文件统计， 显示文件的行数，单词数，字节数， 可用-l、-w、-c分别显示
    du	//查看目录占用空间，-h参数显示适合人类观看格式， --max-depth=x 参数设置显示目录深度
```

**高级指令**

```
查找：

	命令后接 -exec + 指令 {} \;	//将查找到的内容传给后方指令
	接|xargs + 指令 	//将查找到的内容分段传给后方指令，防止溢出
	
	find dir [option] target	//在指定目录下查找目标， 
		-name “XXX(正则)”	按名字查找相应目录下的文件
		-type <类型字母>   按类型查找文件，普通文件特别用f查找
		-size 			 按大小查找
		-maxdepth X		 指定查找

	grep [option] dir/file_name		//过滤内容
		-r	递归子目录

压缩：
	
	zip	XX.zip file_name	//压缩文件，-r参数递归子目录压缩整个目录
	unzip XX.zip	//解压缩
	
	gzip/gunzip		//打包单个文件生成.gz文件
	
	gz文件习惯用tar打包， tar -zcvf xx.gz <原料>
		-zxvf参数解压缩
		其中c表示压缩，x表示解压，z表示压缩方式，v表示显示信息(可省略)
		还有j的压缩方式，生成.bzip2文件
	
	rar a -r newdir dir		//.rar格式压缩， a代表压缩，-r递归子目录，压缩包名（不用加后缀） 原材料
	rar x 	//解压
	
安装软件：

	sudo apt-get update		//	更新/etc/apt/sources.list
	sudo apt-get install tree	//	安装tree命令
	sudo apt-get remove tree	//	卸载tree命令
	sudo apt-get clean		//清理包
	
	
	dpkg根据deb安装包安装软件
	sudo dpkg -i XXX.deb	//安装
	sudo dpkg -r XXX.deb	//移除软件包
	
	rpm命令
		--prefix<目的目录>		指定安装目录
		-ivh	常用安装参数，i显示套件相关信息，v显示指令执行过程，h列出标记
		rpm -e 软件名			卸载软件
	
	
	源码安装
	解压压缩包 -> 进入对应目录执行configure文件 ->	make -> sudo make install安装到系统目录下

防火墙
	
	Ubuntu:
		ufw status		查看防火墙状态
		ufw allow <port>	开放对应端口
	
	centos7:
		firewall-cmd --list-ports	查看开放端口
		
		firewall-cmd --zone=public(作用域) --add-port=80/tcp(端口和访问类型) 				--permanent(永久生效)		
		
		firewall-cmd --zone= public --remove-port=80/tcp --permanent
		
		firewall-cmd --reload		重启
		
		systemctl stop firewalld.service 关闭防火墙
		
	
常用复合指令:
	netstat -apn | grep <port>		查看占用指定网络端口的进程
	kill -9 <pid>			终止对应进程
```



**Vim的使用**

```
在用户家目录(/home/用户名)下面有一个.vimrc
/etc下面也有一个vimrc

命令模式：
	ctrl s:暂停
	ctrl q:退出暂停
	ZZ:	保存退出
	ctrl c:强制停止
	ctrl w/ww:切换到上分屏/下分屏
	光标移动：	

        除了方向键外还能使用hjkl，分别是左下上右。
        0移动到行首，$移动到行尾，gg到文件头，G到文件尾
        移动到指定行 <行数>+G		

    删除：
        u撤销操作
        x删除光标处字符，X删除光标前字符
        dw从光标位置删除单词
        d$从光标位置后删除行，等效于D
        d0从光标位置前删除行
        dgg从光标所在行前删除所有字符(包含本行)
        dG从光标所在行后删除所有字符(包含本行)
        dj删除本行和下一行所有字符
        dk删除本行和上一行所有字符
        dh、dl等效于X、x
        ndd删除n行字符

    复制粘贴：
        nyy	复制n行
        p/P	粘贴，p粘贴到下一行，P粘贴到本行
        ndd 剪切n行 
        r替换字符
        
        v进入可视化模式（选中文本），y复制，p粘贴
        shift + v: 多行选中模式， </>调整缩进
        ctrl + V:区块模式（多列选中），多行注释
	
进入编辑模式：

	aios大小写均可进入编辑模式，8种情况光标位置不同
	
	a:光标后移一位
	A:移动到行末
	i:光标位置不变
	I:移动到行首
	o:下方新建空白行
	O:上方新建空白行
	s:删除当前字符
	S:删除当前行
	esc:退出编辑模式

进入末行模式：
	
	: 进入该模式
	!+ shell指令 可以执行对应指令
	/xxx	从前往后查找xxx， n查找下一个，N查找上一个，	?xxx从后往前查找
	s/xxx/xx/ 将当前行第一个匹配的xxx替换为xx， +g替换整行
	%s/xxx/xx/ 将每一行第一个匹配的xxx替换为xx， +g替换整行
	w	写入(保存)
	q	退出，会询问是否保存
	q!	退出不询问
	x	写入并退出
	sp file_name	上下分屏打开文件/	vsp file_name 左右分屏打开文件
	qall:退出全部文件
```

**SHELL脚本**

```
创建.sh脚本文件
首行#!/bin/bash表示使用bash来执行脚本
#后可以写注释
使用各种shell命令和特定语法结构编写脚本程序
```





**GCC编译流程**



```
gcc xx.c 	编译.c文件生成可执行文件a.out，实际上这个指令经过了几步操作，也可以分别实现
	gcc -E		预处理——头文件展开、宏替换，可使用 重定向 >(清空目标文件再写入)/>>(追加写入) 将生						成代码写入文件，通常为.i文件
	
	gcc -S 		生成汇编指令xx.s文件
	
	gcc -c		生成二进制目标文件xx.o
	
	链接生成可执行文件a.out
	
gcc xx.c -I dir 包含目录	
	调用另一个源文件的函数:
		1.在a.c 里引用"b.c"并声明b.c里的函数
		2.创建b.h，b.h引用"b.c"并声明b.c里的函数，a.c引用"b.h"
		
-o filename 指定生成的文件 
-lstdc++ 编译cpp文件
-g 使用gba调试模式
-Wall 显示所有警告

静态库

    ar rcs libxxx.a xx.o xx.o ...	打包生成静态库文件
    -L包含库目录， -l指定库名

动态库
	
	1.编译与位置无关的代码。生成.o文件，关键参数 -fPIC
	2.将.o文件打包，关键参数 -shared，例： gcc -shared -o libxx.so xx.o
	3.将库文件与头文件一起发布
	
	使用:
	1.与静态库相同的指令编译出可执行文件
	2.正确配置程序依赖的共享库，可以使用 ldd xxx 查看文件所依赖的共享库列表，配置方法有多种
	
		方法一：将共享库.so文件直接移动到/lib目录下或/usr/lib目录下或在上述目录下建立共享库的连接
		
		方法二：将动态库文件路径配置到$LD_LIBRARY_PATH环境变量下，export(生效一次) LD_LIBRARY_PATH 				=dir:$LD_LIBRARY_PATH
		
		(推荐)方法三：将动态库所在目录添加到/etc/ld.so.conf尾行，运行ldconfig指令
```

**Makefile**

```
一次编写，反复使用

命名规则：makefile、Makefile

三要素：目标、依赖、规则命令

默认处理第一个目标
当依赖文件比目标文件新，则重新递归编译生成目标文件
规则前加@隐藏指令
加-指令报错也继续执行
.PHONY: 目标名 	定义伪目标，防止和目录下文件重名出现冲突

写法:

	目标:依赖
	制表符	命令
	
变量:
	value = xx.x xx.x xx.x
	调用: $(value)
	只能在规则中出现的变量：
        $@ 		目标
        $^		所有依赖
        $<		第一个依赖
        $?		第一个变化的依赖
	
函数:
	wildcard 进行文件匹配，例: value = $(wildcard *.c)
	patsubst 替换文件，例： value = $(par subst %.c, %.o, 原料(可以是变量))
	
```

**gdb**

```
gdb调试常用指令:
	gdb file_name 	启动gdb

    set args <参数> 设置程序参数

    r(un)		运行程序

    start		分布调试，从主函数开始，
        n(ext)		进行下一步
        s(tep)		进行下一步，若遇到函数尝试进入

    q(uit)		退出gdb

    list	显示代码段，默认显示十行，默认从主函数所在文件开始 <file_name:行数> 指定文件

    b(reak) 
        <行数>	在主函数所在文件目标行设置断点
        <function_name>		在目标函数设置断点
        <文件名:行数>	在目标文件的目标行设置断点

    i(nfo) b(reak)	查看断点

    d(el) 断点编号	删除指定断点

    c(ontinue)	跳到下一个断点

    p(rint) 变量		查看变量
        ptype 变量		查看变量类型
        
       
gdb跟踪core文件：
	
	ulimit -c	查看core文件大小	unlimited选项不限制core文件大小
	
	gdb <程序名> core 使用core文件
	
	where 查看错误位置
	
修改core文件配置： /proc/sys/kernel/core_pattern
```

**Linux信号**

```
signal信号是进程之间相互传递消息的一种方法，信号全称为软中断信号，也有人称作软中断，从它的命名可以看出，它的实质和使用很象中断。

信号的基本概念 

    软中断信号（signal，又简称为信号）用来通知进程发生了事件。进程之间可以通过调用kill库函数发送软中断信		号。Linux内核也可能给进程发送信号，通知进程发生了某个事件（例如内存越界）。

    注意，信号只是用来通知某进程发生了什么事件，无法给进程传递任何数据，进程对信号的处理方法有三种：

    1）第一种方法是，忽略某个信号，对该信号不做任何处理，就象未发生过一样。

    2）第二种是设置中断的处理函数，收到信号后，由该函数来处理。

    3）第三种方法是，对该信号的处理采用系统的默认操作，大部分的信号的默认操作是终止进程。
   
信号的类型 ：见Picture目录

signal库函数 
	signal库函数可以设置程序对信号的处理方式。

	函数声明：
	sighandler_t signal(int signum, void(*sighandler_t)(int) handler);
		参数signum表示信号的编号。

		参数handler表示信号的处理方式，有三种情况：

			1）SIG_IGN：忽略参数signum所指的信号。

			2）一个自定义的处理信号的函数，信号的编号为这个自定义函数的参数。

			3）SIG_DFL：恢复参数signum所指信号的处理方法为默认值。 

	程序员不关心signal的返回值。
	
信号有什么用

    服务程序运行在后台，如果想让中止它，强行杀掉不是个好办法，因为程序被杀的时候，程序突然死亡，没有释放资源，	 会影响系统的稳定，用Ctrl+c中止与杀程序是相同的效果。
    如果能向后台程序发送一个信号，后台程序收到这个信号后，调用一个函数，在函数中编写释放资源的代码，程序就可以	 有计划的退出，安全而体面。
	信号还可以用于网络服务程序抓包等。
	
	
可靠信号与不可靠信号

	信号分为不可靠信号(1-32)与可靠信号(34-64)。不可靠信号主要有以下问题:

		1）每次信号处理完之后，就会恢复成默认处理
	  	 （早期的signal函数，linux2.6.35.6内核经验证已经不再恢复默认动作)。
	
		2)存在信号丢失的问题(进程收到的信号不作排队处理，相同的信号多次到来会合并为一个)。
	
	现在的Linux对信号机制进行了改进，因此，不可靠信号主要是指信号丢失。
	
信号处理函数被中断
	
	当一个信号到达后,调用处理函数，如果这时候有其它的信号发生，会中断之前的处理函数，等新的信号处理函数执行完	 成后再继续执行之前的处理函数。
	但是，同一个信号会排队阻塞。

信号的阻塞
	
	若收到新的信号后不希望马上处理，可以设置阻塞。
	
	信号集的概念:
		信号集被定义为一种数据类型：
			typedef struct {
                       unsigned long sig[_NSIG_WORDS];
			} sigset_t
			
		信号集用来描述信号的集合，每个信号占用一位（64位）。Linux所支持的所有信号可以全部或部分的出现在信号		 集中，主要与信号阻塞相关函数配合使用。
		
		执行信号的处理动作称为信号递达（Delivery），信号从产生到递达之间的状态，称为信号未决（Pending）。		进程可以选择阻塞（Block）某个信号。被阻塞的信号产生时将保持在未决状态，直到进程解除对此信号的阻塞，		才执行递达的动作。注意，阻塞和忽略是不同的，只要信号被阻塞就不会递达，而忽略是在递达之后可选的一种处		  理动作。每个进程都有一个用来描述哪些信号递送到进程时将被阻塞的信号集，该信号集中的所有信号在递送到进		程后都将被阻塞。
	
	信号阻塞相关函数:
		int sigemptyset(sigset_t *set);
				初始化set指定的信号集，信号集里面的所有信号被清空，相当于64为置0；
				
		int sigfillset(sigset_t *set);
				调用该函数后，set指向的信号集中将包含linux支持的64种信号，相当于64为都置1；
				
		int sigaddset(sigset_t *set, int signum)
				在set指向的信号集中加入signum信号，相当于将给定信号所对应的位置1；

		int sigdelset(sigset_t *set, int signum)；
				在set指向的信号集中删除signum信号，相当于将给定信号所对应的位置0；

		int sigismember(const sigset_t *set, int signum)；
				判定信号signum是否在set指向的信号集中，相当于检查给定信号所对应的位是0还是1

		int  sigprocmask(int  how,  const  sigset_t *set, sigset_t *oldset));
				能够根据参数how来实现对信号集的操作，操作主要有三种：
					SIG_BLOCK 在进程当前阻塞信号集中添加set指向信号集中的信号，相当于：mask=mask|set
					
					SIG_UNBLOCK 如果进程阻塞信号集中包含set指向信号集中的信号，则解除对该信号的阻塞，					相当于：mask=mask|~set
					
					SIG_SETMASK 更新进程阻塞信号集为set指向的信号集，相当于mask=set
		
		int sigpending(sigset_t *set));
				获得当前已递送到进程，却被阻塞的所有信号，在set指向的信号集中返回结果。
				
		int sigsuspend(const sigset_t *mask));
		
		sigaction =======================================================================
		
		struct sigaction{
			void (*sa_handler)(int);
			void (*sa_sigaction)(int, siginfo_t *, void *);
			sigset_t sa_mask;
			int sa_flags;
			void (*sa_restorer void);
		};
		sa_handler 信号处理函数
		
		sa_flags 用来设置信号处理的其他相关操作，下列的数值可用:
		
			SA_RESETHAND：信号处理之后重新设置为默认的处理方式。
			
			SA_RESTART：如果信号中断了进程的某个系统调用，则系统自动启动该系统调用
			
			SA_NOCLDWAIT：使父进程在它的子进程退出时不会收到SIGCHLD信号，这时子进程如果退出也不会成为						 	  僵尸进程。
			SA_NOCLDSTOP：使父进程在它的子进程暂停或继续运行时不会收到 SIGCHLD 信号。
			
			SA_NODEFER ：一般情况下， 当信号处理函数运行时，内核将阻塞该给定信号。但是如果设置了 							SA_NODEFER标记， 那么在该信号处理函数运行时，内核将不会阻塞该信号
			
			 SA_SIGINFO：使用 sa_sigaction 成员而不是 sa_handler 作为信号处理函数。

		int sigaction(int signum, const struct sigaction * act,struct sigaction *oldact);
			
		
```



**Linux多进程**

```
进程的概念
	什么是进程？进程这个概念是针对系统而不是针对程序员的，对程序员来说，我们面对的概念是程序，当输入指令执行一	 个程序的时候，对系统而言，它将启动一个进程。

	进程就是正在内存中运行中的程序，Linux下一个进程在内存里有三部分的数据，就是“代码段”、”堆栈段”和”数据		段”。”代码段”，顾名思义，就是存放了程序代码。“堆栈段”存放的就是程序的返回地址、程序的参数以及程序的局部	  变量。而“数据段”则存放程序的全局变量，常数。

	系统如果同时运行多个相同的程序，它们的“代码段”是相同的，“堆栈段”和“数据段”是不同的（相同的程序，处理的数	   据不同）。

多进程
	
	pid_t fork();
	
		fork函数用于产生一个新的进程，函数返回值pid_t是一个整数，在父进程中，返回值是子进程编号，在子进程		 中，返回值是0。
	
		fork函数创建了一个新的进程，新进程（子进程）与原有的进程（父进程）一模一样。子进程和父进程使用相同的		代码段；子进程拷贝了父进程的堆栈段和数据段。子进程一旦开始运行，它复制了父进程的一切数据，然后各自运		  行，相互之间没有影响。父进程结束后子进程交由系统托管。
	
	int kill(pid_t pid, int sig);
		用来送参数sig 指定的信号给参数pid 指定的进程。参数pid 有几种情况：
            1、pid>0 将信号传给进程识别码为pid 的进程.
            2、pid=0 将信号传给和目前进程相同进程组的所有进程
            3、pid=-1 将信号广播传送给系统内所有的进程
            4、pid<0 将信号传给进程组识别码为pid 绝对值的所有进程参数
            
            
```

**linux多线程**

```
#include<pthread.h>

	int pthread_create(pthread_t *thread,
                       const pthread_attr_t *attr,
                       void *(*start_routine) (void *),
                       void *arg);
                       
	pthread_t *thread：
		传递一个 pthread_t 类型的指针变量，也可以直接传递某个 pthread_t 类型变量的地址。pthread_t 是		  一种用于表示线程的数据类型，每一个 pthread_t 类型的变量都可以表示一个线程。
	
	const pthread_attr_t *attr：
		用于手动设置新建线程的属性，例如线程的调用策略、线程所能使用的栈内存的大小等。大部分场景中，我们都不		  需要手动修改线程的属性，将attr参数赋值为NULL，pthread_create()函数会采用系统默认的值创建线程
	
	 void *(*start_routine) (void *)：
	 	以函数指针的方式指明新建线程需要执行的函数，该函数的参数最多有 1 个（可以省略不写），形参和返回值的			类型都必须为 void* 类型。void* 类型又称空指针类型，表明指针所指数据的类型是未知的。使用此类型指针		   时，我们通常需要先对其进行强制类型转换，然后才能正常访问指针指向的数据。
		如果该函数有返回值，则线程执行完函数后，函数的返回值可以由 pthread_join() 函数接收。
	
	void *arg：
		指定传递给 start_routine 函数的实参，当不需要传递任何数据时，将 arg 赋值为 NULL 即可。
		
		如果成功创建线程，pthread_create() 函数返回数字 0，反之返回非零值。各个非零值都对应着不同的宏，	 指明创建失败的原因，常见的宏有以下几种：
		
	EAGAIN：系统资源不足，无法提供创建线程所需的资源。
	EINVAL：传递给 pthread_create() 函数的 attr 参数无效。
	EPERM：传递给 pthread_create()函数的attr参数中，某些属性的设置为非法操作，程序没有相关的设置权限。
	
	以上这些宏都声明在 <errno.h> 头文件中，如果程序中想使用这些宏，需提前引入此头文件。
	
	int pthread_join(pthread_t thread, void **value_ptr);	阻塞主线程等待对应子线程退出。
        thread：等待退出线程的线程号。
        value_ptr：退出线程的返回状态。
       
线程的终止：

	1.代码运行完成自动消亡,线程状态返回值为15
	2.return void* <返回状态>
	2.void pthread_exit(void *retval);	
	3.被主线程或其他线程终止
	
线程资源的回收：
	
		线程有joinable和unjoinable两种状态，前者当线程终止时不会释放资源，这种线程称为僵尸线程。后者终止	 时会由系统自动释放资源
	
	线程资源的回收有四种方法：
	
		1.调用pthread_join()方法，会产生阻塞因此一般不适用
		
		2.创建线程前调用pthread_attr_setdetachstate将线程设置为detached，该线程退出时由系统回收资源
			pthread_attr_t attr;
			pthread_attr_init(&attr);
			pthread_attr_setdetachstate(&attr, PTHREAD_CREATE_DETACHED);
			pthread_create(&pthid, &attr, pth_main, arg);
		
        3.创建线程后，调用pthread_detach()将对应线程设置为detached状态
        	pthread_detach(pthid);
		
		4.创建线程后，在该线程里调用pthread_detach将自身设置为detach状态
			pthread_detach(pthread_self());
			
线程的取消：

	int pthread_cancel(pthread_t thread);
	取消后线程状态返回-1(PTHREAD_CANCELED)；
	
	子线程可以调用pthread_setcancelstate()设置响应pthread_cancel()的方式
		
		int pthread_setcancelstate(int state, int *oldstate);
			oldstate用于保存旧参数，可以缺省
			默认state为PTHREAD_CANCEL_ENABLE,改为PTHREAD_CANCEL_DISABLE则cancel不生效
	
	调用pthread_setcanceltype来设定线程取消的方式： 
               pthread_setcanceltype (PTHREAD_CANCEL_ASYNCHRONOUS, NULL); //异步取消、 
               pthread_setcanceltype (PTHREAD_CANCEL_DEFERRED, NULL); //同步取消、 
               pthread_setcanceltype (PTHREAD_CANCEL_DISABLE, NULL);//不能取消 
	
线程清理：
	
	终止线程前可能需要完成善后工作
	
	void pthread_cleanup_push(*void(*routine)(void*), void *arg);
		将对应函数压入清理函数栈
	
	void pthread_cleanup_pop(int execute);
		execute为0则只弹出函数，不执行；非零则弹出并执行函数
		线程被cancel或遇到pthread_exit()会执行所有清理函数
		
	清理函数必须成对出现在线程中，否则会报错
	
线程和信号：

	向子线程发送信号用int pthread_kill(pthread_t thread, int sig); 
	
	异常产生的信号（比如程序错误，像SIGPIPE、SIGEGV这些），则只有产生异常的线程收到并处理。
	
	用pthread_kill产生的内部信号，则只有pthread_kill参数中指定的目标线程收到并处理。
	
	外部使用kill命令产生的信号，通常是SIGINT、SIGHUP等job control信号，则会遍历所有线程，直到找到一个不	   阻塞该信号的线程，然后调用它来处理。(一般从主线程找起)，注意只有一个线程能收到。
　　
　　其次，每个线程都有自己独立的signal mask，但所有线程共享进程的signal action。这意味着，你可以在线程中	调用pthread_sigmask(不是sigmask)来决定本线程阻塞哪些信号。但你不能调用sigaction来指定单个线程的信	号处理方式。如果在某个线程中调用了sigaction处理某个信号，那么这个进程中的未阻塞这个信号的线程在收到这个信	号都会按同一种方式处理这个信号。另外，注意子线程的mask是会从主线程继承而来的。
	
```

