---
title: mybatis 参数判断条件
date: 2018-07-19 14:23:09
tags:
  - mybatis
  - java
categories:
  - 随笔
---
mybatis绝对是好用的，但是稍不留神也容易翻船啊喂，
血的教训告诉我各种参数的判断条件一！定！要！写！好！
备份记录如下：
1.判断String是否为空
### `<if test="stringParam != null and stringParam != ''"></if>`### 
2.判断Integer是否大于0
### `<if test="idParam !=null and idParam gt 0"></if>`### 
3.判断List是否不为空
### `<if test="listParam !=null and listParam.size >0"></if>`### 
4.判断String是否以某特定字符(比如此处的"user")开头
### `<if test="stringParam.indexOf('user') != -1"></if>`### 
5.判断字符串是否等于特定字符(比如此处的user)
### `<if test='stringParam != null and stringParam == "user"'></if>`### 

注意不能使用此写法 
###~~`<if test="stringParam != null and stringParam != 'user'"></if>`~~###
 即最外边用双引号，里边用单引号，此写法会报java.lang.NumberFormatException异常

如果要用这个写法要这么写
### `<if test="stringParam != null and stringParam != 'user'.toString()"></if>`###