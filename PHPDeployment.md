简介
===

GoProxy 中的 php fetchserver 使用了 [多种](https://github.com/phuslu/goproxy/tree/master/fetchserver/php) 程序语言实现： Golang, JavaScript, PHP. 任一种都可用来部署。

部署
===

按云计算平台不同，部署步骤会不相同。

OpenShift
------------

+ php fetchserver 所用语言： golang
+ 看视频时下载速度： 供测试的服务端 `https://mygo-yxorpog.rhcloud.com/` , 密码 `123456`

### 步骤

#### 服务端

+ **OpenShift 部分**

	1. 注册 OpenShift 账号： <https://www.openshift.com/app/account/new>
	2. 进入邮箱，如 Gmail <https://mail.google.com>
	3. 找到收件箱中 OpenShift 发来的邮件（若收件箱里没有，有可能会在垃圾箱里），点击 Verify Your Account 字样的链接，然后在打开的页面中点击 Accept
	4. OpenShift 部分至此结束，可放心关掉 OpenShift 相关的网页

+ **Cloud9 IDE 部分**

	1. 注册 Cloud9 IDE 及进入 IDE 环境

		可参考 <https://docs.google.com/document/d/1Wxwl4HrvIpie9xIRRMzasdW_HAuthBFjqL_hQCKBIfE/edit> 中 `步骤` 中的 `注册` 和 `工作空间` 

	2. 进入 IDE 环境后依次书写以下命令：

		- > rhc setup

			然后按回车键，此时会出现 `Enter the server hostname: |openshift.redhat.com|` 的字样，不用管，直接再按一次回车键。然后会出现 `Login to openshift.redhat.com: ` 此时应输入你注册 OpenShift 时所用的邮箱地址，并按回车键，然后输入密码，再回车键。出现 `Generate a token now? (yes|no) ` 输入 yes 后按回车键，再继续输入 yes , 按回车。然后会出现 `Please enter a namespace (letters and numbers only) |<none>|: ` 此时输入你想给空间命的名字，这个名字必须是 OpenShift 中唯一的，如果出现重复会提示你重新命名一个，然后按回车。然后输入下面的命令

		- > rhc create-app mygo https://cartreflect-claytondev.rhcloud.com/reflect?github=ARwMq9b6/openshift-go-cart

			然后按回车，并等待应用创建完成。至此服务端创建完毕，接下进入客户端。

			注意： 
				1. mygo 是应用名，可随意填写
				2. php 默认密码是 [123456](https://github.com/ARwMq9b6/openshift-go-cart/blob/master/template/index.go#L24), 可 fork 后手动修改

#### 客户端

- GoProxy

	1. 下载 <https://github.com/ARwMq9b6/goproxy/archive/config.zip> , 解压后将里面的 `main.user.json` （作用是使 php 优先）和 `php.user.json` 放到 GoProxy 的目录里
	2. 修改 `php.user.json` , 将里面的 `https://mygo-yxorpog.rhcloud.com/` 修改为您自己的——将其中的 `mygo` 替换为您的应用名（若未自定义，默认是 `mygo` ）， `yxorpog` 替换为您的空间名，即 `Please enter a namespace (letters and numbers only) |<none>|: ` 这一步所填写的名字

- 浏览器

	设置代理服务器为 127.0.0.1:8000 类型 https , 若不行就选 http

Heroku
-------

待补充……

可参考 kingtope...@gmail.com 的帖子 <https://code.google.com/p/goagent/issues/detail?id=22048#c10>