##1、更新系统，安装第三方源并更换默认防火墙
###1.1安装第三方源
**如果系统没有安装wget，首先安装wget工具:**
```
sudo yum install wget
```
**远程下载mysql官方源并安装源:**
```
wget http://repo.mysql.com/mysql-community-release-el7-5.noarch.rpm
sudo rpm -ivh mysql-community-release-el7-5.noarch.rpm
```

**执行**`ls -1 /etc/yum.repos.d/mysql-community*`**，如果发现有两个仓库文件存在，如下显示，就说明安装成功:**
```
/etc/yum.repos.d/mysql-community.repo
/etc/yum.repos.d/mysql-community-source.repo
```
###1.2更新系统
```
#更新yum软件包
yum check-update  

#更新系统
yum update
```
###1.3更改默认防火墙，开启3306端口，80端口
**关闭firewall：**
```
systemctl stop firewalld.service #停止firewall
systemctl disable firewalld.service #禁止firewall开机启动
```

**安装iptables防火墙：**
```
yum install iptables-services #安装
sudo vi /etc/sysconfig/iptables #编辑防火墙配置文件
```
**配置文件更改如下：**
```
# Firewall configuration written by system-config-firewall
# Manual customization of this file is not recommended.
*filter
:INPUT ACCEPT [0:0]
:FORWARD ACCEPT [0:0]
:OUTPUT ACCEPT [0:0]
-A INPUT -m state --state ESTABLISHED,RELATED -j ACCEPT
-A INPUT -p icmp -j ACCEPT
-A INPUT -i lo -j ACCEPT
-A INPUT -m state --state NEW -m tcp -p tcp --dport 22 -j ACCEPT

//下面是编辑添加的部分
-A INPUT -m state --state NEW -m tcp -p tcp --dport 80 -j ACCEPT
-A INPUT -m state --state NEW -m tcp -p tcp --dport 3306 -j ACCEPT
//以上是编辑添加的部分

-A INPUT -j REJECT --reject-with icmp-host-prohibited
-A FORWARD -j REJECT --reject-with icmp-host-prohibited
COMMIT

```
然后输入`:wq`保存退出，在命令窗口输入以下命令使其生效：
```
systemctl restart iptables.service #最后重启防火墙使配置生效
systemctl enable iptables.service #设置防火墙开机启动
```
##2、关闭SELINUX
**命令行输入以下内容，打开selinux配置文件：**
```
sudo vi /etc/selinux/config
```
**修改内容如下**
```
#SELINUX=enforcing #注释掉

#SELINUXTYPE=targeted #注释掉

SELINUX=disabled #增加
```
**输入`:wq!` #保存退出,然后命令行输入以下内容，使其生效**
```
setenforce 0 #使配置立即生效
```

##3、安装配置nginx
###3.1 安装
```
yum install nginx #安装nginx
systemctl start nginx #启动nginx
systemctl enable nginx #加入开机启动项
```
### 3.2配置
```
#打开nginx.conf
sudo vi /etc/nginx/nginx.conf

#在http{}配置中加入：
client_max_body_size 1024M;
```
**注意：如果安装nginx的时候，提示没有可用的软件包nginx，需要我们手动配置下，具体细节如下：**
```
#首先下载对应当前系统版本的nginx包(package)：
wget  http://nginx.org/packages/centos/7/noarch/RPMS/nginx-release-centos-7-0.el7.ngx.noarch.rpm

#然后建立nginx的yum仓库：
rpm -ivh nginx-release-centos-7-0.el7.ngx.noarch.rpm

#下载并安装nginx：
yum install nginx

#最后启动和加入开机启动操作：
systemctl start nginx #启动nginx
systemctl enable nginx #加入开机启动项
```
##4、安装和配置PHP

###4.1 安装PHP和相关插件
```
yum install -y php php-cli php-curl php-fpm php-intl php-mcrypt php-mysql php-gd php-mbstring php-xml php-dom
```
**注意：如果缺少部分扩展，请手动编译php扩展，具体方法请自行搜索**
###4.2 修改PHP配置

**编辑php.ini , 将以下配置的值修改为1024M，命令窗口输入**
```
vim /etc/php.ini
```
**编辑内容如下**

```
post_max_size ＝ 1024M
memory_limit ＝ 1024M
upload_max_filesize ＝ 1024M
```
###4.3 配置PHP-FPM
**打开php-fpm配置文件**
```
sudo vi /etc/php-fpm.d/www.conf
```
**修改以下内容**
```
listen.owner = apache
listen.group = apache
listen.mode = 0666
```
**最后**
```
sudo systemctl start php-fpm    #启动php-fpm
sudo systemctl enable php-fpm   #开机启动fpm
```
##5、安装mysql
```
yum install mysql mysql-server  #安装mysql
systemctl restart mysql  #重启刷新mysql
```
**注意：mysql默认用户是root，没有密码，建议手动更改密码**
##6、下载并安装配置edusoho
###6.1 下载安装edusoho
```
wget http://download.edusoho.com/edusoho-6.6.6.tar.gz
tar -xzvf edusoho-6.6.6.tar.gz edusoho
cp -r edusoho /var/www
cd /var/www && sudo chown -R apache:apache ./
```
**注意:给www目录赋予用户权限时，如果提示没有apache这个用户和用户组，请查询服务器的用户组来确认php-fpm进程的用户组**
###6.2 edusoho的配置
**创建配置文件：**
```
server {
    listen 80;

    # [改] 网站的域名
    server_name www.xxxx.com;

    #301跳转可以在nginx中配置

    # 程序的安装路径
    root /var/www/edusoho/web;

    # 日志路径
    access_log /var/log/nginx/example.com.access.log;
    error_log /var/log/nginx/example.com.error.log;

    location / {
        index app.php;
        try_files $uri @rewriteapp;
    }

    location @rewriteapp {
        rewrite ^(.*)$ /app.php/$1 last;
    }

    location ~ ^/udisk {
        internal;
        root /var/www/edusoho/app/data/;
    }

    location ~ ^/(app|app_dev)\.php(/|$) {
        fastcgi_pass   127.0.0.1:9000;
        fastcgi_split_path_info ^(.+\.php)(/.*)$;
        include fastcgi_params;
        fastcgi_param  SCRIPT_FILENAME    $document_root$fastcgi_script_name;
        fastcgi_param  HTTPS              off;
        fastcgi_param HTTP_X-Sendfile-Type X-Accel-Redirect;
        fastcgi_param HTTP_X-Accel-Mapping /udisk=/var/www/edusoho/app/data/udisk;
        fastcgi_buffer_size 128k;
        fastcgi_buffers 8 128k;
    }

    # 配置设置图片格式文件
    location ~* \.(jpg|jpeg|gif|png|ico|swf)$ {
        # 过期时间为3年
        expires 3y;

        # 关闭日志记录
        access_log off;

        # 关闭gzip压缩，减少CPU消耗，因为图片的压缩率不高。
        gzip off;
    }

    # 配置css/js文件
    location ~* \.(css|js)$ {
        access_log off;
        expires 3y;
    }

    # 禁止用户上传目录下所有.php文件的访问，提高安全性
    location ~ ^/files/.*\.(php|php5)$ {
        deny all;
    }

    # 以下配置允许运行.php的程序，方便于其他第三方系统的集成。
    location ~ \.php$ {
        # [改] 请根据实际php-fpm运行的方式修改
        fastcgi_pass   127.0.0.1:9000;
        fastcgi_split_path_info ^(.+\.php)(/.*)$;
        include fastcgi_params;
        fastcgi_param  SCRIPT_FILENAME    $document_root$fastcgi_script_name;
        fastcgi_param  HTTPS              off;
    }
}

```
**重启nginx:**
```
systemctl restart nginx
```
**注意：真实配置要根据自己服务器的实际情况来斟酌修改，不能完全照搬 **

##7、完成
* 如果在命令执行过程中出现提示权限不够(permission denied)，请在前面添加`sudo`;
* 配置中出现的文件目录可以自己规定，但是要更改相应的配置文件。因为linux操作比较复杂。建议linux专业人员进行操作；
* 因为CentOS 7 安装源不够稳定，安装过程中可能会出现软件源不稳定的情况，所以建议使用Ubuntu14.04 或者 CentOS 6.x版本作为服务器；
* 欢迎用户提问题，我们会尽快修正问题；
