---
title: 使用自己的域名访问hexo
date: 2017-01-04 10:12:07
tags: hexo
---

hexo搭建成功还是很赞赞的，但是毕竟访问它还要巴拉巴拉的记住一长串的域名还是很让人忧伤（访问速度还不快~）。作为一个喜欢折腾的程序员，毕竟还是会有自己的域名的，私心想着研究下直接使用[自己的域名 blog.fangbin.me](http://blog.fangbin.me)来访问它。动手！
## 域名添加DNS解析：
前提是需要有一个自己的域名，怎么申请我就不多介绍了，我的域名是[fangbin.me](http://fangbin.me)。
直接在阿里云的域名控制台添加解析如下：
![域名解析][1]

**当然，这里会解释下**：
github官网提供了两个主机ip地址：192.30.252.153 和 192.30.252.154， 将这两个作为主机地址（记录值），给域名的DNS解析添加两个 A记录，
然后再添加一个GNAME记录，主机地址填的是我们原本用来访问 github 博客的地址，比如我的就是 demosbin.github.io

## 创建GNAME文件
在hexo本地目录 source 目录下面新建一个文件，取名为 GNAME (没有后缀)，内容就是自己的域名：
GNAME

    blog.fangbin.me
注意：这里最好直接写 xxxx.com，前面不要加上www,否则就只能访问 www.xxxx.com,而不加的情况下就都能访问了。

OK，到这里就配置完成啦！！！

按照[hexo的文档][2]执行以下指令使修改生效：

    hexo g
    hexo d

然后就可以愉快地通过自己地域名访问hexo了


  [1]: http://on557pwy7.bkt.clouddn.com/dnsjiexi.png
  [2]: https://hexo.io/zh-cn/docs/