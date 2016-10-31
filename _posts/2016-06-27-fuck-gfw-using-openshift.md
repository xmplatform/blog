---
layout: post
title: 利用openshift实现翻墙
categories: mess
tags:
- mess
description: OpenShift是redhat公司推出的一个PaaS云计算应用平台，开发者可以在上面构建、测试、部署和运行应用程序。它支持Java、Ruby、Node.js、Python、PHP、Perl等众多语言环境和开发框架。MySQL,PostgreSQL,MongoDB等数据库服务。

---
##介绍##

- **OpenShift：**
OpenShift是redhat公司推出的一个PaaS云计算应用平台，开发者可以在上面构建、测试、部署和运行应用程序。它支持Java、Ruby、Node.js、Python、PHP、Perl等众多语言环境和开发框架。MySQL,PostgreSQL,MongoDB等。而且它是免费的。

- **翻墙原理**
因为在OpenShift上创建的应用可以通过SSH来访问，而SSH的数据传输又是通过加密传输，因此可以通过socket5把请求代理到本地然后再使用SSH隧道访问目标网页，以此达到翻墙目的。


##配置步骤##

###注册OpenShift，建立一个Appilcation###
- **注册登录OpenShift：**[OpenShift](https://www.openshift.com/app/account/new)

![注册OpenShift](/assets/img/openshift/1.png)

如果注册时看不到验证码可能是被屏蔽了，需要翻墙才能显示。登录时，记住账号、密码，下次登录的时候就不用输验证码。

这里推荐一个翻墙软件以便完成注册：[Green加速器](https://www.getgreenjsq.info/index.php?option=com_user&task=register&affid=3276166)

- **创建一个Application：**

![进入控制台](/assets/img/openshift/2.png)

单击`Add Application` 添加Application。然后选择运行环境，由于只是用来翻墙，所以随便选一个就行了。例如，我选择了PHP5.4运行环境。

![选择运行环境](/assets/img/openshift/3.png)

![](/assets/img/openshift/4.png)
###配置OpenShift SSH###
- **下载PuTTY和PuTTYgen：**其中前者是用作SSH连接，后者是生成SSH的私钥和公钥。下载地址：
[PuTTY和PuTTYgen](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html)

- **配置SSH**

首先打开PuTTYgen，点击`Generate`生成公钥。（PS：鼠标在进度条下面上下滑动生成速度会快。）
然后复制生成的公钥到本地。然后点击`Save private key`,将生成的ppk格式的私钥保存好。

 ![](/assets/img/openshift/5.png)

- **在OpenShift上添加SSH公钥**

![](/assets/img/openshift/6.png)

添加公钥：

![](/assets/img/openshift/7.png)

接下来是把Source Code里的这段字符串复制到本地，等一下要用到。

![](/assets/img/openshift/8.png)

- **配置PuTTY**

填上上一步复制的字符串中的主机名。

![](/assets/img/openshift/9.png)

将这里的0改成60，意思是每过60s请求一次服务器，因为如果三、四分钟都没有新请求的话就会断开连接。

![](/assets/img/openshift/10.png)

填上上面保存的字符串里面的用户名（也就是`//`与`@`之间的内容）。

![](/assets/img/openshift/11.png)

选择刚才导出的ppk格式的私钥。

![](/assets/img/openshift/12.png)

配置本地端口转发，端口数值要：1024<端口<65535。

![](/assets/img/openshift/13.png)

最后保存设置，给当前设置起名，下次要用该设置直接load就行了。

![](/assets/img/openshift/14.png)

点击open，第一次打开会有安全警告，直接接受就行了。当看到下面这个画面时说明已经配置好了。

![](/assets/img/openshift/15.png)

###配置浏览器Socks 5代理###

我使用火狐浏览器，进入到附加组件里面搜索`代理`或`proxy`随便下一个。我选择了Foxy Proxy，设置好Socks 5代理。
其他浏览器的组件自行百度。

![](/assets/img/openshift/16.png)

##成功翻墙##
- **Google**

![](/assets/img/openshift/17.png)

- **YouTube**

![](/assets/img/openshift/18.png)

- **Instagram**

![](/assets/img/openshift/19.png)

