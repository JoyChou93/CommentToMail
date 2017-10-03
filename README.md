
# Typecho 评论邮件提醒插件

访客评论后，将会发送评论内容到您指定的邮箱。


## 使用说明

1. git clone代码到`/usr/plugins/`目录
2. 进行后台配置，建议配置成如下配置。163邮箱可使用密码，QQ需要使用授权码。

![setting](http://o8jiujmnw.bkt.clouddn.com/Typecho-CommentToMail-Setting.png)


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

有两种方法处理fsockopen发送HTTP请求失败的问题：

1. 加上`usleep`函数。可看到的返回码依然是499.
2. nginx配置中加上`fastcgi_ignore_client_abort on;`也能解决失败的问题。此时返回码是200.

测试发现，异步请求fsockopen比curl快，因为不用等CURL的那一秒。

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

## 引用

- [http://www.cnblogs.com/52fhy/p/6209479.html](http://www.cnblogs.com/52fhy/p/6209479.html)
