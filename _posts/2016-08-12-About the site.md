-
layout: post
title:  关于站点大致说明
date:   2016-08-12 20:00:00 +0800
tag: 博客 网站
---
之前的博客空间到期了，迁到了这里，记录部分要点于下：

### 关于github的配置

准备工作：在github申请一个账号，然后创建一个名为<用户名>.github.io的仓库，比如我的用户名是haochuang，那么我的仓库名字就是haochuang.github.io

首先，下载配置git，我用的ubuntu16.04系统，所以在终端中键入：

> sudo apt-get install git

开始安装，如果安装过程提示缺少某些依赖包，按照提示一个个安装即可，其他系统请参考[官网说明][1]。
安装完git之后在本地创建一个名字和你刚刚创建的仓库名字一样的文件夹，比如我刚刚创建的仓库名为haochuang.github.io，本地文件夹名字也就是haochuang.github.io，然后用git初始化此目录，并添加远程仓库。

在ubuntu16.04命令行模式下操作为：

> mkdir haochuang.github.io  
  cd haochuang.github.io  
  git init  
  git remote add git@github.com:uesrname/username.github.io.git

为了以后推送方便设置ssh，配置请参考[如何创建git公钥][2]。
git相关配置已经完成，接下来就是正式的搭建博客。

### 首先简单说明一下jekyll是什么
    
Jekyll 是一个简单的博客形态的静态站点生产机器。它有一个模版目录，其中包含原始文本格式的文档，通过一个转换器（如 Markdown）和Liquid渲染器转化成一个完整的可发布的静态网站，你可以发布在任何你喜爱的服务器上。Jekyll 也可以运行在 GitHub Page 上，也就是说，你可以使用 GitHub 的服务来搭建你的项目页面、博客或者网站，而且是完全免费的。

### jekyll的基本目录结构

> ├── _config.yml  
  ├── _drafts  
  |   ├── begin-with-the-crazy-ideas.textile  
  |   └── on-simplicity-in-technology.markdown  
  ├── _includes  
  |   ├── footer.html  
  |   └── header.html  
  ├── _layouts  
  |   ├── default.html  
  |   └── post.html  
  ├── _posts  
  |   ├── 2007-10-29-why-every-programmer-should-play-nethack.textile  
  |   └── 2009-04-26-barcamp-boston-4-roundup.textile  
  ├── _site  
  ├── .jekyll-metadata  
  └── index.html

简单介绍一下他们的作用：

> _config.yml  
 保存配置数据

> _drafts  
 保存未发布的草稿

> _includes  
 可以用来存放一些小的可复用的模块，方便通过{ % include file.ext %}（去掉前两个{中或者{与%中的空格，下同）灵活的调用。

> _layouts  
 layouts（布局）是包裹在文章外部的模板。布局可以在 YAML 头信息中根据不同文章进行选择。

> _posts  
 文章存放位置

> _site  
 这个是Jekyll生成的最终的文档，不用去关心。最好把他放在你的.gitignore文件中。

> .jekyll-metadata  
 该文件帮助 Jekyll 跟踪哪些文件从上次建立站点开始到现在没有被修改，哪些文件需要在下一次站点建立时重新生成。最好把它加入.gitignore文件中。

> index.html  
 如果这些文件中包含 YAML 头信息 部分，Jekyll 就会自动将它们进行转换。

### jekyll的配置

jekyll的配置写在_config.yml中，具体配置有很多，在此放出我的配置，更详细的内容请参考[jekyll的官方配置文档][3]

> title: 念槐聚  
subtitle: 个人世界  
description: 欢迎来到我的世界~  
avatarTitle: haochuang  
avatarDesc: 勿忘初心  
# url: "www.uetest.com"  
comment:  
social:  
    weibo:  
    github: haochuang  
    twitter:   
    mail:  
 baidu:  
    id: HAOCHUANGTEST99091988822  
    id: UA-98133145-1   
    host: auto   
permalink: /:year/:month/:title/  
highlighter: rouge  
textColor: #FF000  
cover_color: clear  
blog_button:  
    title: 博客主页  
nav:  
    - {title: 所有文章, description: archive, url: '/archive'}  
    - {title: 标签, description: tags, url: '/tags'}   
    - {title: 关于我, description: about, url: '/about'}  
 gems: [jekyll-paginate]  
paginate: 20  
paginate_path: "page/:num/"  

### 如果不想自己配置模板怎么办

可以去[这里][4]寻找自己中意的模板，或者你也可以直接fork[我的模板][5]，然后把源码下载下来稍加修改之后放到刚才创建的本地目录里面。

### 如何修改

1.修改配置文件  
首先打开
 _config.yml文件，修改如下选项：

* titile:你的博客标题
* subtitle:你的博客子标题
* description:你的博客描述
* avatarTitle：你的头像里的标题
* avatarDesc：你的头像描述
* url:改成你的域名
* comment里的duoshuo:改成你的多说的用户名
* social里面的
* weibo：你的微薄id（不是用户昵称）
* github：你的github用户名
* mail:你的邮箱
其他的可以补充，没有的可以不写，将原文中的删除即可
* baidu: id：你的百度统计的id
* ga: id:你的Google Analytics的id

2.修改个人介绍文件
 about.md

在里面写上一段自我介绍就好

3.头像

打开images文件夹，将你自己的头像文件改名为
avatar.jpg

4.网站图标

如果你想使用自己的个性网站图标，同样的将你的图标图片放在该文件夹，并重命名为favicon.png

5.博客文章

打开
_posts文件夹，将其清空，然后把自己写的文章放进去。
这里面，你在新建博客时必须包含前6行的内容，其中title后写博客标题，date后时间（但格式要保持一致），tag后写标签。后面的内容则是markdown语法的内容。 将上述文件保存，命名为：2016-08-04-MyFirstBlog.md即可。


推送到远程仓库：

> cd username.github.io  
git add remote username.github.io  
git add -A  
git commit -m "build blog"  
git push

注：这里的“username”指你的github用户名

这样博客就被部署在github上了，过十分钟左右就可以通过ghcc.github.io进行访问。

### 关于自定义域名
我用的是[.tk](http://www.dot.tk)的免费域名haochuang.tk,申请完域名之后记得在nameserver里面添加几条A记录，然后在github的仓库设置页面github pages栏目下面可以直接填入你刚刚申请的域名。   
ps：使用github提供的域名可以使用github pages自带的强制https加密选项，如果是自定义域名只能自己安装ssl加密证书。



    
### 部分可参考站点
  [1]: https://pages.github.com/
  [2]: https://gist.github.com/yisibl/8019693
  [3]: http://jekyllcn.com/
  [4]: https://github.com/jekyll/jekyll/wiki/Sites
  [5]: https://github.com/haochuang/haochuang.github.io
  [6]:http://jekyllcn.com/docs/templates/