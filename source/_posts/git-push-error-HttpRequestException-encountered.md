---
title: git push时的异常HttpRequestException_encountered
date: 2018-05-13 08:56:58
tags:
  - hexo
  - git
categories:
  - 随笔
---

今天随手发布hexo的时候发现`hexo d` 居然失败，报出了 `fatal: HttpRequestException_encountered` 这种奇怪的异常，随手push一个项目，发现 `git push` 也是失败的，异常大概长下面这样：
![HttpRequestException_encountered][1]

这就问题大了！git出问题了？查一下~~果然：
![git 官方答疑][2]
大意是说git禁用了对弱加密（TLSv1/TLSv1.1）的支持，windows用户不能进行身份验证，然后需要升级git到[2.16以上的新版本][3]，如果还是不行的话，得更新[git的管理凭证][4]
随手更新了下，发现果然OK了！（只更新了管理凭证，只更新了管理凭证，只更新了管理凭证！重说三）

再次附上地址：
git新版下载地址：[https://github.com/git-for-windows/git/releases][5]
管理凭证GCM下载地址：[https://github.com/Microsoft/Git-Credential-Manager-for-Windows/releases/tag/v1.15.2][6]


  [1]: http://on557pwy7.bkt.clouddn.com/hexo/image/gitError.png
  [2]: http://on557pwy7.bkt.clouddn.com/hexo/image/gitErrorResolve.png
  [3]: https://github.com/git-for-windows/git/releases
  [4]: https://github.com/Microsoft/Git-Credential-Manager-for-Windows/releases/tag/v1.15.2
  [5]: https://github.com/git-for-windows/git/releases
  [6]: https://github.com/Microsoft/Git-Credential-Manager-for-Windows/releases/tag/v1.15.2