---
title: "技术：小白从零用Hugo搭建个人网站遇到的问题一览"
date: 2022-05-11T19:37:47+08:00
author: "张晶"
slug: website-building-trouble-shooting
draft: false
toc: true
---

大概2022年3月，因为上海封城我封闭在家中，有了很多的时间，决定给自己搭建一个个人网站，来应对之后入学Master、做简历等。首先，我在[B站视频](https://www.bilibili.com/video/BV1cv411N7kz?spm_id_from=333.337.search-card.all.click)中学习了用什么来搭建个人网站。由于我没有租用服务器的想法， 那么看起来很简单很容易上手的Typecho，Halo都被我排除了，剩下的只有Hexo和Hugo。这两个都是静态网页，能够落到github上也比较符合我的需求。

所以我就开始研究怎么搭建一个Hugo个人网页。

大体过程基本上基于[郝鸿涛个人博客中这篇《如何零基础免费搭建个人网站》](https://hongtaoh.com/cn/2021/03/02/personal-website-tutorial/) ，给了我很大的帮助，在遇到困难的时候也在上面求助了郝鸿涛很多！特别感谢！

## 开始搭建之前

我是一个彻彻底底的零基础，对编程的了解仅限于大学的基础编程课，which means我不知道HTML是什么、没有GitHub账号、没有用过git、也不会用markdown。

因此，先要做四件事情。

1. 注册一个GitHub账号
2. 下载一个Markdown的文本编辑器并学习Markdown的基础语法
   - 原因是之后所有的网站内容都会用Markdown来书写和搭建。我在尝试了几种编辑器之后，选了Markdown最好用的编辑器Typora，它有几个优点：文本和大纲可以同时显示；敲下来的语法，可以立刻显示为最终想要呈现的样子，对于初学者特别友好。
   - 关于Markdown的基础语法，我还是找了[B站视频](https://www.bilibili.com/video/BV1hJ411X75X?spm_id_from=333.337.search-card.all.click)，从代码块开始学，并且在Typora上面反复写几遍。反复写几遍也不能保证不出错，我在最后出现错误的时候才发现我一开始练习的插入图片的语法就是错误的。所以多练习是没错的。
3. 下载一个用于html的文本编辑器（我用的是sublime text），方便修改后面的html
4.  （optional）这一步optional，但如果你是一个像我一样彻底的编程小白，是很有必要看一下这一步的。我在运行安装的时候，总是出现一串错误代码：

```java
xcrun: error: unable to load libxcrun (dlopen(/Library/Developer/CommandLineTools/usr/lib/libxcrun.dylib, 0x0005): tried: '/Library/Developer/CommandLineTools/usr/lib/libxcrun.dylib' (mach-o file, but is an incompatible architecture (have 'x86_64', need 'arm64e')), '/usr/lib/libxcrun.dylib' (no such file)).
```

这段让人比较困惑，我就拿到Stackoverflow上查了一下，发现我根本没有安装xcode开发展工具。解决这个问题需要在终端输入：

```java 
xcode-select --install 
```
下载 Xcode Command Line Tools

然后就可以用git了。

5. 为了正确地使用博客中的comment功能，需要提前安装utteranc.es，可以根据[这份指南](https://mscipio.github.io/post/utterances-comment-engine/)来做，只需要坐到第三步即可。在原本的partial—>footer文件中已有需要的script。

## 在搭建和更新中需要注意

在搭建中同样有一些需要注意的地方。

1. 如果你像我一样在中国大陆地区使用了VPN并进行git更新，那么在建立过程中可能会屡次出现以下的错误代码：

   ```java
   Fatal: fatal: unable to access 'https://github.com/xxx': OpenSSL SSL_connect: SSL_ERROR_SYSCALL in connection to github.com:443
   ```

   这是由于使用了代理。我们需要输入:

   ```java
   git config --global --unset-all remote.origin.proxy
   ```

   这个代码可以消除behind a proxy的影响。

2. 如何查看自己的deploy失败的原因

   如果你有绑定GitHub至自己的邮箱，或者你本来就是用自己某一邮箱注册的GitHub，那么出现失败，你会直接收到一份邮件，并打开邮件查看自己run失败的原因，然后进行修改。

   此外，还可以通过在repository—>code处点击commit，看自己失败还是成功。绿色的对勾代表已经部署成功，红色的叉号代表部署失败了。



## 如果有需要修改layout

1. 我遇到的第一个需要修改的问题就是在搭建完网页之后，首页下方的评论中依然是郝鸿涛网页中的评论。这个原因是在`layouts` -> `partials` -> `footer.html` 里用的是他的 repo，这里需要把这行链接换成自己的。

2. 方便增加图片的方法：

   可以在`static` （static放在根目录下即可）中新建一个文件夹， 比如image或者picture之类的，挑自己喜欢的名字。之后再加入图片的话可以在帖子中这样加：
   ```java
   {{figure src= "/images/image.jpg" title = "blablabla" caption = "blablabla" width = "xxx"}}
   ```

   

3. 需要修改Logo

   在建完网站后，网站默认的是左上角的Hugo-logo，但是可能我们并不喜欢。这时需要找到文件夹themes—>static—>media，并找到其中的Hugo-logo.png。这时你需要自己建一个新的png的文件，即设计一个你自己的logo。我打开photoshop然后随便画了个自己的。

   然后把config.toml文件中params中的favicon中的hugo-logo.png改为你新建的这个png文件。params.logo这里同步改。

   

4. 需要修改网站的名字

      依然是在params.logo这里，修改alt这行

      

   

