### 作用介绍
Bash和其它大多数shell使用Readline库作为其输入相关的库。Readline库有一些默认的键盘映射，除此之外，也可以通过修改inputrc文件来定制键盘映射。  


inputrc文件时Readline库的启动文件，当使用Readline作为输入库的程序启动时，它会自动读取inputrc配置文件，初始化自定义的键盘映射。  


inputrc文件的位置由shell的环境变量INPUTRC控制，如果该变量没有设置，缺省的 inputrc 文件的路径是~/.inputrc。  


如果该文件~/.inputrc 不存在，就会使用系统级(对所有用户生效)的inputrc文件/etc/inputrc。如果某个用户需要修改系统默认的 inputrc 配置，可以改动~/.inputrc，这样会覆盖系统的默认配置。  

### inputrc 配置  

在inputrc文件中，有两种配置：一种是inputrc变量，一种是键盘映射。 注意，在配置该文件时，注释必须占单独的一行，否则可能会有问题。



详细参考：https://www.chuchur.com/article/mac-linux-case-sensitive  


