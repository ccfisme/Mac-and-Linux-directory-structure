* 第一步，打开shell并登录后，会先读入全局环境变量设定档/etc/profile

可看其内部：  
![image](https://user-images.githubusercontent.com/74129445/142346844-f2acebdd-3e39-415b-add3-ae649427ecc0.png)  


* 第二步，根据不同使用者帐号，于其家目录内读取~/.bash_profile;读取失败则会读取~/.bash_login;再次失败则读取~/.profile(这三个文档设定基本上无差别，仅读取上有优先关系);  

*  最后，根据用户帐号读取~/.bashrc  

当登入系统时候获得一个shell进程时，其读取环境设定档如下  

![image](https://user-images.githubusercontent.com/74129445/142346937-bdc656eb-c69d-4875-a53a-a5f49939480f.png)  

更多信息参考：https://www.jianshu.com/p/a57e8f1a3426

