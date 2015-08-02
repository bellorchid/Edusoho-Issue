**如何优雅的安装GitBook？**

##安装Gitbook

###依赖工具
>想要更好的管理自己的Nodejs环境，我推荐大家用下面的方式安装Nodejs，首先说一下依赖的包：
* nvm(nodejs version manager)
* npm(nodejs package manager)
* nodejs

####依赖环境安装
> 如果你此前已经通过其他方式安装了nodejs再执行此步骤的话，可能会产生冲突，请`卸载掉之前的安装痕迹` 或者 `跳过此步`）

* [ nvm安装方式参考](https://github.com/creationix/nvm)

* 第一步：终端输入`curl -o- https://raw.githubusercontent.com/creationix/nvm/v0.25.4/install.sh | bash`

* 第二步：关闭终端，再重新打开，就可以使用`nvm`命令了，或者直接在终端输入`source ~/.bash_profile`或者`source ~/.bashrc`（是`.bash_profile`,`.profile`, 或者 `.zshrc`还是`.bashrc`取决于你的配置文件的名称，请自行查看），这样会重新载入terminal配置文件。

* 第三步：在终端输入`nvm install 0.12`(0.12是版本号，也可以安装0.11，0.10等版本，gitbook要求至少0.10以上版本的nodejs),静静等待nvm帮我们安装nodejs，因为nodejs已经自带npm，所以我们不用再安装了
>注意：由于nodejs的镜像来自于国外服务器，可能会速度有些慢，我们可以指定从国内镜像安装，详情点击[这里](wewew)

* 第四步：设置系统默认nodejs版本，在terminal输入`nvm alias default 0.12`(0.12是你想要设置的的版本号)。


####安装Gitbook

* 安装方式官方说的很明白，请自行参考：[ Gitbook安装方式参考](https://github.com/GitbookIO/gitbook)
>由于npm的镜像源也在国外服务器，如果你安装不成功的话，建议使用国内服务器淘宝镜像，详情请点击[这里]()


**不保证以上说的会因为过时或者文档本身存在错误，欢迎即时向我错误反馈**
