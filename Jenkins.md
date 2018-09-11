
#### 1.什么是Jenkins ?


#### 2.Jenkins的启动和关闭
启动和关闭很简单。
Jenkins是使用war包来启动的，自带了Tomcat。输入以下命令就可以启动了。

    这条命令指定了内存和端口
    nohup java -Xms1024m -Xmx1024m -XX:PermSize=512M -XX:PermSize=1024M -jar jenkins.war --httpPort=8090

    这条命令只是指定了端口
    nohup java -jar jenkins.war --httpPort=8090

只需要在访问地址后加上exit，然后进行访问就可以关闭了。




#### 3.Jenkins的安装和使用

##### 1）安装


安装启动了Jenkins后，如果启动的时候，没有网络连接安装不了插件，就需要在启动后安装插件。

安装SSH插件,为了用SSH连接服务器,上传文件到服务器,执行命令。

登陆后，选择 系统管理-->管理插件。

![选择](https://github.com/franck418/Tool_Guide/blob/master/Jenkins/1.png)



选择 可选插件（这个过程有点慢）--> 搜索SSH ---> 勾选Publis Over SSH --->点击 直接安装
![选择](https://github.com/franck418/Tool_Guide/blob/master/Jenkins/2.png)


安装完成后结果如下：
![选择](https://github.com/franck418/Tool_Guide/blob/master/Jenkins/3.png)


虽然有错误的提示,但是最后也可以正常安装和正常使用。估计这两个错误是由于服务器没有翻墙导致的.


然后去配置需要上传的服务器: 选择系统管理 --> 系统设置 --> 往下找到 Publish over SSH 并填写内容。

![选择](https://github.com/franck418/Tool_Guide/blob/master/Jenkins/4.png)

参数说明
Passphrase：SSH的密码
使用用户名/密码登录时为用户名的密码，使用私钥登录时为私钥的密码。
Path to key：SSH私钥的文件路径
私钥文件的路径，可以是绝对路径，也可以是相对$JENKINS_HOME的相对路径
Key：私钥
私钥导出后的文本内容

如果“Key”和“Path to key”都设置，则“Key”的优先级较高，私钥的密码是“Passphrase”中设置的内容。
Disable exec：禁止在目标机上执行命令

可以点高级,来填写端口号。没有写的话就是默认的22.

填写完成资料后,点击Test Configuration来测试一下是否能够正常连接。如果提示Success则表示可以正常连接。

最后点保存就可以了。


下面开始创建一个构建项目。

选择新建项目， 输入名称后，选择构建一个自由风格的软件项目，然后确定。

接下来就是比较关键的配置了。

基本的描述写完以后,就要配置关键的源码管理了。这里我使用的是SVN。如果源码这里没有 Subversion这个选项的话，就要像安装SSH插件那样去到插件
管理那边，搜索 Subversion。然后安装。

Credentials 是凭据，就是SVN的账号和密码，如果没有的话就要点击旁边的的Add添加一个。

填写完成后如下所示：

![SVN填写完成](https://github.com/franck418/Tool_Guide/blob/master/Jenkins/5.png)


构建触发器 选择轮询

![SVN填写完成](https://github.com/franck418/Tool_Guide/blob/master/Jenkins/6.png)

*/1 * * * *  这个代表1分钟1次


最后选择构建后的操作步骤， 选择Send build artifacts over SSH。就是构建完成后通过SSH连接上传文件到服务器。



Remote directory 这个文件夹地址是基于服务器基本文件夹上面的。

例如服务器基础文件夹是/home/jenkins/  ， Remote directory 值又写了/test/的话。 那么文件将会上传到/home/jenkins/test/文件夹。

服务器基础文件夹是添加服务器的时候，设置的。

最后配置上传完成后的文件复制命令。

cp -rf 源文件夹夹路径 目标文件夹路径

