在CentOS 安装 JDK


在CentOS安装JDK比较在Windows安装方便很多，用一句命令就可以搞定了。 也不用配置环境变量。


1 输入命令
```
yum search jdk
```
来查看有哪些JDK可以安装。 如下图：


![查看JDK](https://github.com/franck418/Tool_Guide/blob/master/img/1.png)


2 输入命令

```
 yum install java-1.8.0-openjdk.x86_64
```
来进行JDK1.8的安装。

中途会提示一共下载XXM， 输入y回车。就会继续安装了。


3 等待安装完毕后，输入命令 java -version 来检验是否安装成功。

![安装成功](https://github.com/franck418/Tool_Guide/blob/master/img/2.png)


默认会安装在 /usr/lib/jvm 目录中

这样JDK1.8就安装好了。




