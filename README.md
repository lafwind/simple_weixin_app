### 一个微信公众号app

利用Rails实现的一个公众号app。

##### 运行

因为运行公众号需要在外网有服务器及相应的域名（填写URL和Token需要），所以可以利用ngrok让微信公众平台访问本机运行的rails server，下面为具体步骤：

* 下载[ngrok](https://ngrok.com/)，需要注册。然后在Dashboard获得自己的Authtoken，比如xxxxxxxxxx，然后执行如下语句（参看Dashboard内容）：

  ```shell
       $ ./ngrok authtoken xxxxxxxxxx
  ```
* 进入app根目录，运行`rails server`

* 运行如下代码，获得一个类似 `http://abcdefg.ngrok.io` 的网址
  ```shell
      $ ./ngrok http 3000
  ```
* 打开`app/config/initializers/weixin_rails_middleware.rb`，去掉`config.weixin_token_string`和`config.weixin_secret_string`之前的注释（这些内容是添加gem后自动生成的）

* 前往微信公众平台接口测试帐号申请[网页](http://mp.weixin.qq.com/debug/cgi-bin/sandbox?t=sandbox/login)，申请后进入管理测试号页面。

* 在`接口配置信息`的URL处填入`"http：//abcdefg.ngrok.io/weixin/"` + `"#{config.weixin_secret_string}"`的值

* 在下面的Token中填入`"#{config.weixin_token_string}"`的值

* 保存。

这样公众号就运行起来了（测试用的），然后用自己的微信号关注该测试公众号，就能使用该公众号的功能了。


##### 功能

* 对输入的长句子进行翻译，中英文皆可

* 对输入的短词进行字典查询，中英文皆可

##### Todo list

* 对输入的地址，返回该地址的相关天气信息

* 其他
