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











































































































 






















