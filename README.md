
# Typecho 评论邮件提醒插件

>访客评论后，将会发送评论内容到您指定的邮箱。

原作者是  DEFE (http://defe.me)。


## 使用说明

1. 下载插件

2. git clone代码到`/usr/plugins/`目录

3. 后台配置
	- 建议端口配置465，25端口测试邮件发送失败 
	- 由于写日志需要php用户的写权限，需要对插件目录`chmod -R 777`

## 升级日志

#### v3.0.0 

1. 修复使用Socket发送HTTPS请求失败的BUG
2. 修复使用Curl方式发送HTTP或者HTTPS请求失败的BUG
3. 修复Action.php不获取控制台是否写日志的配置，导致日志写入不成功Bug
4. 修改随机文件为12位，增强安全性
5. 修改日志中发送的邮箱为明文


## 邮件发送实现原理

1. 将评论的POST请求记录到`cache/12位随机字符串`文件中
2. 通过Socket或者Curl请求`/action/comment-to-mail?send=12位随机字符串`
3. `action.php`收到请求后，读取cache文件里的内容后删除cache文件，并发送邮件

## 测试环境

typecho 1.0 (14.10.10)

## 说明

fsockopen发送HTTP请求时，加上`usleep`函数后，邮件会发送成功，可看到的返回码依然是499。如果想处理这个499返回码问题，可以在nginx配置中加上`fastcgi_ignore_client_abort on;`。参考[http://www.cnblogs.com/52fhy/p/6209479.html](http://www.cnblogs.com/52fhy/p/6209479.html)

## 运行结果

```
[INFO] 2017-10-03 01:18:08
[INFO] 开始发送请求：https://joychou.org/action/comment-to-mail?send=IyfYsO3GZ1qR
[INFO] Socket方式发送HTTP请求……
[INFO] 开始发送邮件……
[INFO] Socket方式发送HTTP请求结束！
[INFO] 向joychou@joychou.org发送邮件成功！
[INFO] 2017-10-03 01:18:09 邮件发送完毕!
```
