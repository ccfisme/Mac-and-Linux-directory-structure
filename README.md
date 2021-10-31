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

* Applications

![截屏2021-10-31 18 50 38](https://user-images.githubusercontent.com/74129445/139579199-eb7b9271-d557-4fe7-84c7-dcc6d8e06047.png)  

这没什么说的，就是我安装的那些软件  

* Users  

![截屏2021-10-31 18 52 38](https://user-images.githubusercontent.com/74129445/139579304-84236a7b-2b6c-443c-b1a5-a10417d1a950.png)  

这应该就是我这个用户，不知道里面是干什么的，试试看  

![截屏2021-10-31 19 30 07](https://user-images.githubusercontent.com/74129445/139580892-640f5394-13d8-43a4-ae01-ccb4faa127bb.png)  


wdf,为什么又有一个library？我得查查有几个library，要区分好  

**一个是根目录下的Library**  

![截屏2021-10-31 19 20 21](https://user-images.githubusercontent.com/74129445/139580479-5d903080-0d56-4c02-bca8-ac85033075be.png)  

本地库：位于/Library/由系统上的所有用户共享，并存储各种资源。属于计算机上的所有用户，但仅管理员和root用户可以访问。在大多数情况下，您应该没有理由访问二级库。  



**一个是system下的Library**  

![截屏2021-10-31 19 21 20](https://user-images.githubusercontent.com/74129445/139580534-0b559ea9-e4db-4813-b392-f50f7ddaf7af.png)  

系统库：位于/System/Library/处，用于存储操作系统。它是只读的，以保护系统（尽管超级用户可以进行更改），因此不会像其他库文件夹那样存储任何首选项文件  



**一个是用户目录下的Library(注：～等价于/User/ccf,也就是home目录，系统默认为～)**  

![截屏2021-10-31 19 23 28](https://user-images.githubusercontent.com/74129445/139580648-7e20af58-ebe4-4c19-b6f1-1c0daaabb98e.png)  

用户库：位于Macintosh HD/Users/youruseraccount/Library/您最需要熟悉的库。它更新最频繁，因为它存储应用程序首选项、应用程序支持文件、缓存等  



* cores

![截屏2021-10-31 19 34 44](https://user-images.githubusercontent.com/74129445/139581091-f77d2322-f69d-450e-962d-49573ba2f26e.png)  

？？？？  

我不李姐，为什么什么都没有？？  

搜索：https://www.jianshu.com/p/a2f10010b384  

发现这是一个gcc段错误（段错误应该就是访问了不可访问的内存，这个内存区要么是不存在的，要么是受到系统保护的，参考：https://www.cnblogs.com/hello--the-world/archive/2012/05/31/2528326.html） 后产生错误信息的文件，真的假的？？我试试  

根据提示  

![FireShot Capture 036 - 如何在mac上分析coredump文件 - 简书 - www jianshu com](https://user-images.githubusercontent.com/74129445/139581211-a26114b6-63d2-4211-82a1-e68c2b82af33.png)  

我先写个错误  





































 






















