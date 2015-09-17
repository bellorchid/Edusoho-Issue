##Edusoho发布方式

**1、演示站升级http://exam.edusoho.cn/**



**2、执行从演示站点拉取edusoho_init.sql 和 资源文件的命令**

`app/console topxia:dump-init-data exam.edusoho.cn exam.edusoho.cn edusoho exam.edusoho.cn`
```
a.执行完后会在installFiles下生成edusoho_init.sql，data.zip，data/ 文件和目录；

b.会把edusoho_init.sql拷贝到web/install下；

c.参数1：服务器地址，参数2：数据库用户名，参数3：数据库密码，参数4：数据库

```

**3、app/console topxia:build**

**4、app/console topxia:copy-install-files 6.4.1**

> c.参数1：版本号



**5、人肉测试**
