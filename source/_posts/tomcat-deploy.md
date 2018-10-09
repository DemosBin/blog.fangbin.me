---
title: tomcat的三种部署方式
date: 2018-08-24 16:13:29
tags:
  - tomcat
  - server
categories:
  - 服务器
---
研究了下公司项目的打包部署方式，跟着命令走就发现了项目部署的路径怪怪的，并不在tomcat目录下，以前没细了解，就一并查了下tomcat的部署方式，有以下三种：

1.最常见方式：项目war包或者解压后直接放到tomcat/webapp目录下，启动tomcat访问

2.修改 tomcat/config/server.xml文件，指定部署目录
在<Host></Host>标签之间输入
<Context path="/" docBase="/Data/deploy/app/" reloadabel="false" >
path:浏览器访问时的路径名
docBase:web项目的WebRoot所在的路径，注意是WebRoot的路径，不是项目的路径。其实也就是编译后的项目
reloadble:设定项目有改动时，tomcat是否重新加载该项目

3.在tomcat/conf/Catalina/localhost目录下新建xml文件，文件内容：
<Context  docBase="D:/WebProject" reloadable="true" />
在浏览器输入路径：localhost:8080/xml文件名/访问的文件名
eg: 127.0.0.1:webproject/index.jsp即可访问

总结：
①、第一种方法比较普通，但是我们需要将编译好的项目重新 copy 到 webapps 目录下，多出了两步操作
②、第二种方法直接在 server.xml 文件中配置，但是从 tomcat5.0版本开始后，server.xml 文件作为 tomcat 启动的主要配置文件，一旦 tomcat 启动后，便不会再读取这个文件，因此无法再 tomcat 服务启动后发布 web 项目
③、第三种方法是最好的，每个项目分开配置，tomcat 将以\conf\Catalina\localhost 目录下的 xml 文件的文件名作为 web 应用的上下文路径，而不再理会 <Context>中配置的 path 路径，因此在配置的时候，可以不写 path。
通常我们使用第三种方法，也是我司使用的方式