
##一键试用问题汇总

####```修改时间：2015-09-17```

###1.为什么没有 powered by edusoho?

> 这个问题在develop分支上也有，要等待去排查，看看谁改动了这个地方


###2.安装的版本中含 /install/ 目录，赶紧删除，有安全问题。

> 因为一件试用为非常规步骤安装，所以未执行删除install目录的操作，需要在云平台部署完成后，删除掉

###3./admin/setting/cloud/key/update 还是可以看到key的，赶紧修复。

> 这个地方属于edusoho的范畴，之前没有考虑到这个页面的访问

###4.上回定得是access key为开源版，但开通商业版的功能。

> 这个我不清楚

###5.edusoho后台生成的体验管理员账号的email地址应该是我申请时候填的email地址。

> 初始化账户的时候应该把用户填入的邮箱当做账户邮箱，云平台需要检查初始化数据的步骤,包括要和官网传过来的数据对接

###6.[http://www.edusoho.com/product/probation/stepOne/0](http://www.edusoho.com/product/probation/stepOne/0) 底部的链接地址没一个对啊。

> edusoho官网需要修改
