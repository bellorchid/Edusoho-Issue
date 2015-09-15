## Windows系统下一键安装EduSoho

>为了解决 EduSoho 用户不熟悉技术，安装难度大的问题，EduSoho 官方推出基于UPUPW Apache服务套件的EduSoho 绿色一键安装包。

```注意：本安装包仅适用于测试及体验，不适用于实际产品环境。产品环境推荐使用Ubuntu系统，请参看教程 http://www.qiqiuyu.com/course/20。```



#### **只需以下几个简单步骤，即可轻松安装EduSoho：**


* 从本课时的资料下载区中下载UPUPW EduSoho Apache 一键安装包（点击页面右侧的“资料”图标即可进入资料区）。

* 解压安装包到C盘根目录下，打开文件夹”先装运行库再开启”，运行VC++的库文件, 并确保系统中已安装必要的.NET运行库。

* 以管理员权限运行UPUPW.exe，输入4，先检测Apache服务器默认的80端口和MySQL默认的3306端口是否被占用。如果输入4，如下图所示，说明端口未被占用。（端口如果被占用，请更改端口，或者输入kk清理使用该端口的进程，再执行后续步骤）
![](http://7xjexf.com1.z0.glb.clouddn.com/upupw30003CE7-493C-4565-803A-21F020BC6BE0.png)

* 确认端口无误后，在UPUPW主菜单列表中输入s1，启动所有的服务。确保无错误信息产生。如下图所示
![](http://7xjexf.com1.z0.glb.clouddn.com/upupw82B745DA-8DEC-40A6-B27E-5E1CF961DE13.png)

* 再次在UPUPW主菜单列表中输入4，记录mysql的端口号，如下图（端口号默认3306，如果3306无法解除占用,会使用9999端口，此步骤用来确认端口号）
![](http://7xjexf.com1.z0.glb.clouddn.com/upupw012B9872-9D48-4AB1-AA7B-C28257E30663.png)

* 打开浏览器输入`http://localhost`,根据提示进行Edusoho的安装,输入正确的数据库端口和账户密码，既可以体验我们的Edusoho了（第二部需要输入数据库信息，端口号需要填入上一步显示的端口号，账户密码请去“密码相关.txt”内获取）。
