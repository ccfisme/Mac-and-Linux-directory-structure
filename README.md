# 根目录“/”  

macos系统的目录结构和Linux有些类似，由一个最大的目录‘/’开始，那么这个目录包括什么呢？  

我使用命令进行查看：  


![截屏2021-10-31 18 44 57](https://user-images.githubusercontent.com/74129445/139578961-897cb9cc-a600-438f-bdc4-51daf9014f0b.png)  

发现里面包含了很多我不清楚的一些子目录，我搜了一下，用法分别如下：  

* /bin 传统unix命令的存放目录，如ls，rm，mv等。  


* /sbin 传统unix管理类命令存放目录，如fdisk，ifconfig等等。  


* /usr 第三方程序安装目录。  


* /usr/bin, /usr/sbin, /usr/lib，其中/usr/lib目录中存放了共享库（动态链接库）。  


* /etc. 标准unix系统配置文件存放目录，如用户密码文件/etc/passwd。此目录实际为指向/private/etc的链接。  


* /dev 设备文件存放目录，如何代表硬盘的/dev/disk0。  


* /tmp 临时文件存放目录，其权限为所有人任意读写。此目录实际为指向/private/tmp的链接。  


* /var 存放经常变化的文件，如日志文件。此目录实际为指向/private/var的链接。  


* /Applications 应用程序目录，默认所有的GUI应用程序都安装在这里；  


* /Library 系统的数据文件、帮助文件、文档等等；  


* /Network 网络节点存放目录；  


* /System 他只包含一个名为Library的目录，这个子目录中存放了系统的绝大部分组件，如各种framework，以及内核模块，字体文件等等。  


* /Users 存放用户的个人资料和配置。每个用户有自己的单独目录。  


* /Volumes 文件系统挂载点存放目录。  


* /cores 内核转储文件存放目录。当一个进程崩溃时，如果系统允许则会产生转储文件。  


* /private 里面的子目录存放了/tmp, /var, /etc等链接目录的目标目录。  


* /installer.failurerequests 可能是用来记录发生crash时的日志  


实在是太多了，我的实践里根本没有这么多，我准备一一试试看  






# /Applications

![截屏2021-10-31 18 50 38](https://user-images.githubusercontent.com/74129445/139579199-eb7b9271-d557-4fe7-84c7-dcc6d8e06047.png)  

这没什么说的，就是我安装的那些软件  




# /Users  

这应该就是我这个用户，不知道里面是干什么的，试试看  

![截屏2021-10-31 18 52 38](https://user-images.githubusercontent.com/74129445/139579304-84236a7b-2b6c-443c-b1a5-a10417d1a950.png)  


存放用户的个人资料和配置（我的就是ccf）。每个用户有自己的单独目录。  


![截屏2021-10-31 19 30 07](https://user-images.githubusercontent.com/74129445/139580892-640f5394-13d8-43a4-ae01-ccb4faa127bb.png)  


wdf,为什么又有一个library？我得查查有几个library，要区分好  

**一个是根目录下的Library**  

![截屏2021-10-31 19 20 21](https://user-images.githubusercontent.com/74129445/139580479-5d903080-0d56-4c02-bca8-ac85033075be.png)  

本地库：位于/Library/由系统上的所有用户共享，并存储各种资源。属于计算机上的所有用户，但仅管理员和root用户可以访问。在大多数情况下，您应该没有理由访问二级库。  



**一个是system下的Library**  

![截屏2021-10-31 19 21 20](https://user-images.githubusercontent.com/74129445/139580534-0b559ea9-e4db-4813-b392-f50f7ddaf7af.png)  

系统库：位于/System/Library/处，用于存储操作系统。它是只读的，以保护系统（尽管超级用户可以进行更改），因此不会像其他库文件夹那样存储任何首选项文件  



**一个是用户目录下的Library(注：～等价于/User/ccf/,也就是home目录，系统默认为～)**  

![截屏2021-10-31 19 23 28](https://user-images.githubusercontent.com/74129445/139580648-7e20af58-ebe4-4c19-b6f1-1c0daaabb98e.png)  

用户库：位于Macintosh HD/Users/youruseraccount/Library/您最需要熟悉的库。它更新最频繁，因为它存储应用程序首选项、应用程序支持文件、缓存等  



# /cores

![截屏2021-10-31 19 34 44](https://user-images.githubusercontent.com/74129445/139581091-f77d2322-f69d-450e-962d-49573ba2f26e.png)  

？？？？  

我不李姐，为什么什么都没有？？  

搜索：https://www.jianshu.com/p/a2f10010b384  

发现这是一个gcc段错误（段错误应该就是访问了不可访问的内存，这个内存区要么是不存在的，要么是受到系统保护的，段错误参考：https://www.cnblogs.com/hello--the-world/archive/2012/05/31/2528326.html） 后产生错误信息的文件，真的假的？？我试试  

根据提示  

![FireShot Capture 036 - 如何在mac上分析coredump文件 - 简书 - www jianshu com](https://user-images.githubusercontent.com/74129445/139581211-a26114b6-63d2-4211-82a1-e68c2b82af33.png)  

（关于上图中的ulimit解释：https://www.cnblogs.com/klb561/p/10575043.html）  



我先写个错误  

。。。。写不出来，我的gcc好像和他们的不一样，兴许是太高级了，他们都是用的ubuntu（Linux）来写C语言，gcc版本也都是10.0.01之类的，但都说这个文件是存错误信息的，暂且这么以为吧。

---

## 修正

艹，我就说了出不来，那是软件崩溃才有的错误报告，cores是内核转储文件存放目录。当一个进程崩溃时，如果系统允许则会产生转储文件。  


  

![截屏2021-10-31 20 39 18](https://user-images.githubusercontent.com/74129445/139583692-835e1a57-bdb3-4095-a17b-c71d45b75a6d.png)  



# /home
![截屏2021-10-31 20 37 18](https://user-images.githubusercontent.com/74129445/139583577-509f8f2e-f0c9-49f7-abd0-0be131767c49.png)  

又是空的  

![截屏2021-10-31 20 43 46](https://user-images.githubusercontent.com/74129445/139583882-f68dc441-7a65-4bb1-8442-5bf590845827.png)  

又是屌用没有



# /sbin 

![截屏2021-10-31 20 45 37](https://user-images.githubusercontent.com/74129445/139583954-b4976f1c-2b79-44fb-8d69-91df4fde9bc1.png)  

这个里面的东西倒是非常的多，不知道是干什么用的，看了一些文章后不禁一句卧槽，这他妈就是遗留的历史问题而已  

了解知识点前提：挂载点--即磁盘文件系统的入口目录，说人话就是像‘/’、‘sbin’、‘usr’这种  



* 首先讲一下[历史遗留问题](https://www.osnews.com/story/25556/understanding-the-bin-sbin-usrbin-usrsbin-split/)  

**历史原因**就是之前的存储器代价高昂，所以Linux存文件目录的磁盘（即根目录）只有1.5M，不过麻雀虽小，五脏俱全，里面有所有的子目录如/bin, /sbin, /lib, /tmp.. 后来用户安装的程序太多了，就导致了磁盘不够用，于是就在原来的基础上再添一个磁盘（当然不会太大，有可能还是1.5M，总之是以代价最小的方法，通过多加一个磁盘来解决问题，而不是研发新的大容量磁盘），第二个磁盘叫usr，然后把第一块磁盘（即根目录）的内容分开，即第一块磁盘存系统的程序目录，第二块磁盘存用户的程序目录，两个盘的结构完全相同，再后来，两个盘也不够了，但系统程序目录没必要分开，因为永远那么点，所以把第二块磁盘分开，改成第二块磁盘只存用户程序目录，第三块磁盘（其名为home）存用户数据目录，即usr存用户程序目录，home存用户数据目录（Mac不是这种结构，本段文字只是配合Linux理解Mac的usr存储结构），**注意**，此时的usr盘结构与根目录已经不同了  

然而，这样的分区导致了许多的问题，即后面新开的磁盘存目录时的命名，比如一开始工程师觉得/usr/local用于特定安装文件。然后有人决定/usr/local 不是安装新软件包的好地方，所以让我们添加 /opt等，这就导致文件存储目录的命名没有逻辑感，并且多出来许多新的命名  



* 其次讲一下根目录下的sbin具体存的是什么东西以及一些实际的例子  

sbin文件夹是保存引导、恢复、恢复和修复系统所需的二进制文件  

![FireShot Capture 041 - 了解 Mac 的系统文件夹 - 让技术更简单 - www maketecheasier com](https://user-images.githubusercontent.com/74129445/140016906-3b18a2b9-e184-4a5c-82c0-574e2c60999b.png)

  
  
# /var  

首先，照例是先看看里面有东西吗  

![截屏2021-11-03 14 22 50](https://user-images.githubusercontent.com/74129445/140017180-4e2d3cff-c0f5-450e-85ab-6e0fe4e7d66f.png)  

好，有东西，所以我又继续探索  

“/var”包含系统在其操作过程中写入的文件，如缓存、数据库和日志。var表示variable，并且通常只由核心级系统应用写入。在 macOS 上，**“/var”符号链接到“/private/var”**。  

最后一句有点疑惑，var究竟是‘/’下的，还是‘/private’下面的？  

我分别对根目录下的var文件和private文件下的var文件进行访问

![截屏2021-11-03 14 28 11](https://user-images.githubusercontent.com/74129445/140017521-14d43f95-f674-4144-be6e-94ed0c98c665.png)  

看来都是一个  

# /Library  

前面已经对根目录下的library，/system下的library，以及/User下的library分别进行了区分  


**一个是根目录下的Library**  

![截屏2021-10-31 19 20 21](https://user-images.githubusercontent.com/74129445/139580479-5d903080-0d56-4c02-bca8-ac85033075be.png)  

本地库：位于/Library/由系统上的所有用户共享，并存储各种资源。属于计算机上的所有用户，但仅管理员和root用户可以访问。在大多数情况下，您应该没有理由访问二级库。  



**一个是system下的Library**  

![截屏2021-10-31 19 21 20](https://user-images.githubusercontent.com/74129445/139580534-0b559ea9-e4db-4813-b392-f50f7ddaf7af.png)  

系统库：位于/System/Library/处，用于存储操作系统。它是只读的，以保护系统（尽管超级用户可以进行更改），因此不会像其他库文件夹那样存储任何首选项文件  



**一个是用户目录下的Library(注：～等价于/User/ccf/,也就是home目录，系统默认为～)**  

![截屏2021-10-31 19 23 28](https://user-images.githubusercontent.com/74129445/139580648-7e20af58-ebe4-4c19-b6f1-1c0daaabb98e.png)  

用户库：位于Macintosh HD/Users/youruseraccount/Library/您最需要熟悉的库。它更新最频繁，因为它存储应用程序首选项、应用程序支持文件、缓存等    


# /Volumes

先看看是啥  

![截屏2021-11-03 14 51 13](https://user-images.githubusercontent.com/74129445/140019438-eef64f86-4b40-40d0-b075-aa242aee77d7.png)  

奥，就是磁盘目录（文件系统挂载点存放目录）  


# /dev  

首先看看干什么的：  

![截屏2021-11-03 15 47 27](https://user-images.githubusercontent.com/74129445/140024583-47687e64-395f-4f16-abb6-34a5a18155f8.png)  

。。。看不懂，又去查了查，应该是硬件设备名称的存放目录吧，即：  


/dev 设备文件存放目录，如代表硬盘的/dev/disk0



# /opt 

首先，老生常谈，看一看里面有啥  

![截屏2021-11-03 21 53 34](https://user-images.githubusercontent.com/74129445/140072926-94211b76-79cd-4190-a503-6ab6605f6829.png)  
巴嘎，啥都没有，我又得自己查着理解了  

查的是用于保存附加应用程序安装包的文件。。。？？？？  

为啥我没有？对了，啥是附加应用？我查查  

emmm，越查越多，我大致理解的是opt里面存的是操作系统，并且这个操作系统不是本机提供的，而是自己研发或者下载的  

更为具体的理解：https://unix.stackexchange.com/questions/11544/what-is-the-difference-between-opt-and-usr-local



# /tmp  

先是看了看里面的内容  

![截屏2021-11-04 09 18 46](https://user-images.githubusercontent.com/74129445/140241231-2529d62f-b488-4056-9b09-106618e3f317.png)  

好像是和应用有点关系，查一下  

```
/tmp

一个目录，可供需要一个位置来创建临时文件的应用程序使用。应允许应用程序在此目录中创建文件，但不应假定此类文件在应用程序调用之间保留。

```

看来是用来给应用程序留的创临时文件的地方  

参考:https://unix.stackexchange.com/questions/30489/what-is-the-difference-between-tmp-and-var-tmp?rq=1





# /System  

先是看了看里面的内容  

![截屏2021-11-04 09 21 27](https://user-images.githubusercontent.com/74129445/140241462-222451a4-d162-484c-93e5-4f4cc94ef9b0.png)  

好杂呀，我查了一下，里面存的东西确实杂，有字体，控制面板，首选项之类的   

![截屏2021-11-04 09 24 56](https://user-images.githubusercontent.com/74129445/140241744-6fa7d660-871c-4cda-99b5-aa954b01ecd1.png)  

参考：https://www.google.com/search?q=what%27s+mac%27s+system+folder&sxsrf=AOaemvJ5QI4SEfeH6MxRmFX71xkn48piTQ%3A1635988977059&ei=8TWDYav6AoOymAXN2KTwBg&oq=what%27s+mac%27s+system+folder&gs_lcp=Cgdnd3Mtd2l6EAxKBAhBGAFQ3whY4yxgmT1oAXAAeACAAcICiAH3DJIBBzAuMS41LjGYAQCgAQHAAQE&sclient=gws-wiz&ved=0ahUKEwjrttXuxf3zAhUDGaYKHU0sCW4Q4dUDCA4


# /bin  

看看里面有啥： 

![截屏2021-11-04 09 25 39](https://user-images.githubusercontent.com/74129445/140241860-fa9dee65-86bb-4a56-b20d-d6b07049e786.png)  

卧槽，全是命令，我查查都有什么用  

找了一个多一点的，终端下的命令，在这些命令中包含了bin命令：https://www.jianshu.com/p/3291de46f3ff  

还有个英文版：  

```
cat	Utility to concatenate files to standard output
chgrp	Utility to change file group ownership
chmod	Utility to change file access permissions
chown	Utility to change file owner and group
cp	Utility to copy files and directories
date	Utility to print or set the system data and time
dd	Utility to convert and copy a file
df	Utility to report filesystem disk space usage
dmesg	Utility to print or control the kernel message buffer
echo	Utility to display a line of text
false	Utility to do nothing, unsuccessfully
hostname	Utility to show or set the system's host name
kill	Utility to send signals to processes
ln	Utility to make links between files
login	Utility to begin a session on the system
ls	Utility to list directory contents
mkdir	Utility to make directories
mknod	Utility to make block or character special files
more	Utility to page through text
mount	Utility to mount a filesystem
mv	Utility to move/rename files
ps	Utility to report process status
pwd	Utility to print name of current working directory
rm	Utility to remove files or directories
rmdir	Utility to remove empty directories
sed	The `sed' stream editor
sh	The Bourne command shell
stty	Utility to change and print terminal line settings
su	Utility to change user ID
sync	Utility to flush filesystem buffers
true	Utility to do nothing, successfully
umount	Utility to unmount file systems
uname	Utility to print system information

```  

此英文版参考：https://www.pathname.com/fhs/pub/fhs-2.3.html#BINESSENTIALUSERCOMMANDBINARIES  

# /etc  

看看里面有啥：  

![截屏2021-11-04 09 40 48](https://user-images.githubusercontent.com/74129445/140243068-ba2562e7-c572-4acb-b0d4-ff9267c67554.png)  


东西好多，且不认识，查了查，说是全是配置文件（配置文件”是用于控制程序运行的本地文件），哦，这就是那个环境变量，但是是系统程序的环境变量  

![FireShot Capture 043 - Linux中的etc目录下的文件 - 程序员大本营 - www pianshen com](https://user-images.githubusercontent.com/74129445/140243524-4a8f2235-bca2-438c-9a6a-4dfb846a1015.png)   

参考：https://www.pianshen.com/article/8507429486/  

# /private  

首先，还是先看一下有什么  

![截屏2021-11-04 10 05 08](https://user-images.githubusercontent.com/74129445/140246219-a57644ff-e75e-4289-9587-b30568775065.png)  

显然，这几个文件之前都出来过，所以我怀疑这几个private下的文件就是根目录下的那几个文件，于是我挑了一个进行测试  

![截屏2021-11-04 10 05 13](https://user-images.githubusercontent.com/74129445/140246408-e11ba2ef-759c-4b5b-b446-f64f6da05afb.png)  

果然，事实就是我所预料的那样，但究竟是干什么的，由自面意思，我猜测这是指的权限不可访问，即属于私密文件，只有固定的通路可以访问，现在进行验证  

```
“/private”包含守护进程和命令行工具配置、缓存、变量、虚拟内存交换文件、临时文件和睡眠映像。一些 Unix 系统文件夹，如“/etc”和“/tmp”，它们的内容被符号链接到 /private 中的同名目录。
```
以上文本参考：https://www.maketecheasier.com/understanding-mac-system-folders/


# usr  

**最重点的来了！！！**  

先看里面有啥：  

![截屏2021-11-04 10 29 49](https://user-images.githubusercontent.com/74129445/140254024-baf4ceff-9df5-4c16-b9bd-a3075e937aa5.png)  

好，现在的任务就是弄清楚每个分别是干什么的  

参考：https://tldp.org/LDP/Linux-Filesystem-Hierarchy/html/usr.html

































































































 






















