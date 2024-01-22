---
title: 使用hexo+github+netlify搭建个人博客
tags:
  - hexo
  - github
categories: hexo
cover: 'https://raw.gitmirror.com/rimdl/pic/master/pic4.png'
abbrlink: dc01
date: 2023-12-27 14:00:00
updated: 2023-12-27 21:00:00
---
# 开端

> 最近看到网上关于搭建博客的教程比较多，所以打算使用hexo+github+netlify来搭建个人博客。

# 环境搭建

> 1.注册[github](https://github.com/)
- 新建一个仓库用于存放hexo源码，可以选择私有仓库，netlify上可以使用私用仓库进行构建项目。

> 2.下载安装[git](https://git-scm.com/download)
- 安装及配置教程请百度。

> 3.下载安装[node.js](https://nodejs.org/en/)
- 确保安装"npm"。

# webstorm
> 编辑器选择
- 由于我没事就折腾点项目，所以安装了WebStorm，所以这个项目也就使用了WebStorm。其他编辑器如：VSCode都可以达到同样的效果，我仅以WebStorm为例。

> 项目配置
- 打开WebStorm，新建项目，选择从`GET FROM VCS`导入.
- ![pic1](https://raw.gitmirror.com/rimdl/pic/master/20231227161758.png)
- 选择github账户，此时需要你进行登录，按照提示登录即可。
- ![pic2](https://raw.gitmirror.com/rimdl/pic/master/20231227161945.png)
- 登录完成后，选择克隆刚刚新建的项目，保存到自己本地。

# hexo

> 1.安装hexo
- 打开WebStorm，选择`Terminal`，输入`npm install -g hexo`

> 2.初始化hexo
- 打开WebStorm，选择`Terminal`，输入`hexo init`

> 3.启动
- `hexo server`

> 生成静态文件
- `hexo generate`

- 此时，hexo已布置完成，使用git push到仓库即可。

# netlify

- 打开[netlify](https://www.netlify.com/)，使用github账号进行注册并登录
- 进入首页，点击Add new site ![netlify_add](https://raw.gitmirror.com/rimdl/pic/master/20231227185636.png)
- 选择`Import an existing site`![netlify](https://raw.gitmirror.com/rimdl/pic/master/20231227185756.png)
- 再点击`Deploy with GitHub` ![netlify](https://raw.gitmirror.com/rimdl/pic/master/20231227185921.png)
- 此时会让你使用github授权，许可即可。
- 之后就能看到你的仓库中的项目了。![netlify](https://raw.gitmirror.com/rimdl/pic/master/20231227190217.png)
- 点击新建的hexo项目，会打开配置页面，默认情况下，只需要配置以下两项即可。![netlify](https://raw.gitmirror.com/rimdl/pic/master/20231227190515.png)
  - Build Commend: `npm run build`
  - Publish directory: `public`
- 没有问题后，点击`Deploy xxx`，等待部署完成，部署成功之后，会默认生成一个域名，可以到配置页面修改你自己喜欢的名字，或者添加自己的域名。

# 结束
- 到此，一个hexo+github+netlify的个人博客就搭建完成了。如何写文章，如何美化，后续再说了。