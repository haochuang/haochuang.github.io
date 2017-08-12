---
layout: post
title:  用owncloud打造属于你自己的云端硬盘
date:   2017-06-21
tag: vps 服务
---
### 一.安装准备

1.准备一台已经安装了cent os7的vps，确保80端口和22端口已经打开，并且允许远程连接。  
2.准备好一个自己用的顺手的ssh远程连接软件，我用的是[remmina远程连接](https://github.com/FreeRDP/Remmina/wiki)  
3.OwnCloud 跨平台支持 Windows、Mac、Android、iOS、Linux 等平台，而且还提供了网页版和 WebDAV 形式访问，因此你可以在任何电脑、手机上都能轻松获取上传文件，所以毫无疑问选择它。

### 二.开始搭建
1.在[owncloud官网](https://doc.owncloud.org/server/latest/admin_manual/installation/linux_installation.html)找到[一键包下载地址](https://download.owncloud.org/download/repositories/stable/owncloud/),ssh连接上vps，并键入：

	rpm --import https://download.owncloud.org/download/repositories/stable/CentOS_7/repodata/repomd.xml.key

以root身份运行以下命令添加存储库并安装：

	wget http://download.owncloud.org/download/repositories/stable/CentOS_7/ce:stable.repo -O /etc/yum.repos.d/ce:stable.repo
	yum clean expire-cache
	yum install owncloud

一路下来全部选yes，下载速度可能有点慢，耐心等待或者去喝杯茶即可
如果还有问题请翻阅[owncloud管理手册](https://doc.owncloud.org/server/latest/admin_manual/installation/)

完成之后重启Apache服务器：

	service httpd start

开机自启动：

	chkconfig httpd on

### 三.一些设置

接下来在浏览器输入ip/owncloud就可以看到登录界面，第一次登录时会要求设置管理员账号密码，至此，属于自己的云盘就搭建完成了。


### 四.开始上传
owncloud桌面端，手机端下载，[官网链接](https://owncloud.org/install/#install-clients)，不过需要注意的是在谷歌应用商店和ios应用商店里面的owncloud客户端并不免费，需要支付0.99美刀才能下载。


