
## Typecho 评论邮件提醒插件

>访客评论后，将会发送评论内容到您指定的邮箱。

原作者是  DEFE (http://defe.me)。


### 使用说明

1. 下载插件
2. git clone代码到`/usr/plugins/`目录
3. 后台进行相关配置
4. 建议端口配置465，25我测试都失败 
5. 由于写日志需要php用户的写权限，需要对插件目录`chmod -R 777`

### 升级日志

#### v3.0.0 

1. 修复使用Socket请求url失败的Bug。
2. 使用curl方式发送HTTP或者HTTPS请求，所以目前可能不支持Windows。
3. 修改Action.php不获取控制台是否写日志的配置，导致日志写入不成功Bug。
4. 修改随机文件为8位


### 邮件发送实现模式

1. 将评论的POST请求记录到`cache/8位随机字符串`文件中
2. 通过Socket或者Curl请求`/action/comment-to-mail?send=5asDbmZ`
3. `action.php`收到请求后，读取cache文件里的内容，并发送邮件。

### 测试环境

#### typecho版本 

1.0 (14.10.10)

#### 发件箱

- 网易、QQ都测试通过，均采用465端口
- QQ使用客户端的授权码
- 网易使用密码
- 均采用SSL加密


