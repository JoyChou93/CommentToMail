
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

1. 修复使用Socket发送HTTPS请求失败的Bug。
2. 使用Curl方式发送HTTP或者HTTPS请求。
3. 修复Action.php不获取控制台是否写日志的配置，导致日志写入不成功Bug。
4. 修改随机文件为12位，增强安全性。
5. 修改日志中发送的邮箱为明文


## 邮件发送实现原理

1. 将评论的POST请求记录到`cache/12位随机字符串`文件中
2. 通过Socket或者Curl请求`/action/comment-to-mail?send=12位随机字符串`
3. `action.php`收到请求后，读取cache文件里的内容后删除cache文件，并发送邮件。

## 测试环境


typecho 1.0 (14.10.10)

## 运行结果

```
[INFO] 2017-10-03 00:10:02
[INFO] 开始发送请求：https://joychou.org/action/comment-to-mail?send=rWzIDYWzQJ4V
[INFO] 开始发送邮件…
[INFO] 向xxx@qq.com发送邮件成功！
[INFO] 2017-10-03 00:10:07 邮件发送完毕!
```
