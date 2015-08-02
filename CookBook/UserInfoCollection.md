*前言：如何来收集用户的访问信息？可不可以做到我们可以通过一套后台收集我们所有客户的用户信息？*

##关于Piwik的研究
###一、Piwik依赖要求
####基本配置需求
> WebServer : Apache,Nginx,IIS等

> PHP Version >= 5.3.3 (2015年底Piwik升级到3.0.0，将放弃对PHP5.3的支持，最低支持版本为PHP5.4)

> MYSQL Version >= 4.1

>PHP extension :([pdo](http://php.net/pdo) & [pdo_mysql](http://php.net/pdo_mysql)) || ([mysqli extension](http://www.w3school.com.cn/php/php_ref_mysqli.asp))

####推荐配置

> 想要更大限度的(To make the most out of)使用Piwik，你好需要额外的PHP扩展，推荐的列表如下:

> `php5-curl php5-gd php5-cli php5-geoip`

> 如果你的网站每天只有几百的流量，那你完全不需要担心Piwik的效率，当然，如果你的网站每天有上千乃至更大的流量，你需要优化你的Piwik，优化配置会在之后给大家讲解：[Piwik 配置优化](http://piwik.org/faq/new-to-piwik/faq_137/#faq_137)


####MySQL用户配置

```
$ mysql -u adminusername -p
mysql> CREATE DATABASE piwik_db_name_here;
mysql> CREATE USER 'piwik'@'localhost' IDENTIFIED BY 'password';
mysql> GRANT SELECT, INSERT, UPDATE, DELETE, CREATE, DROP, ALTER, CREATE TEMPORARY TABLES, LOCK TABLES ON piwik_db_name_here.* TO 'piwik'@'localhost';
```
* 创建的用户需要有SELECT, INSERT, UPDATE, DELETE, CREATE, DROP, ALTER, CREATE TEMPORARY TABLES, LOCK TABLES的权限

* 如果可以的话，数据库里尽量只建立Piwik的表。

####推荐的主机

> 推荐高性能的主机来安装Piwik，可以考虑使用官方提供的付费主机服务，[Piwik Host](http://piwik.org/hosting/).

###二、安装Piwik
