---
title: 利用GitHub给博客搭建一个图床
tags:
  - github
categories:
  - 技术
cover: >-
  https://raw.gitmirror.com/xinsi-tecool/mypic/main/c665826d-89d1-4551-8c4d-7a0917cd8506.png
toc: true
comment: true
aging: true
aging_days: 30
share: true
reward: true
abbrlink: 4bbf
date: 2024-01-15 14:51:15
updated: 2024-01-15 14:51:15
---
# 开头
- 我的博客使用的是Markdown格式，所以文章中的图片就可以使用链接的形式添加，这时拥有一个属于自己的图床就非常重要了，本文就如何利用github搭建图床进行说明。
******
# 搭建步骤
## github
- 首先在github中创建一个**公开仓库**用于存放图片，然后点击这个[链接](https://github.com/settings/tokens)去获取token（注意：这个token只会显示一次，一定要保存好，否则就只能重新生成）
******
> 详细步骤
1. 点击上方链接后跳转到此处，点击`Generate new token(classic)`![获取token](https://raw.gitmirror.com/xinsi-tecool/mypic/main/9ae83adc-781d-4c97-86f1-4cf4d450d4cb.png)
2. `Note`随便填写，`Expiration`选择过期时间，选择`No expiration`表示永不过期，之后再勾选上`repo`这个复选框，如图中所示。![获取token](https://raw.gitmirror.com/xinsi-tecool/mypic/main/2b15f147-6273-49dc-925f-eab1183a215f.png)
3. 滑倒最下方，点击Generate token。![获取token](https://raw.gitmirror.com/xinsi-tecool/mypic/main/e372ed90-343e-4e32-961c-0b5aec5c105e.png)
4. 最后就可以看到生成的`token`了，复制下来保存即可。![获取token](https://raw.gitmirror.com/xinsi-tecool/mypic/main/4da5c972-9838-4a7e-bfd9-d8b833ae8c7a.png)
******
## 客户端
- 较多人使用的有[PicGo](https://github.com/Molunerfinn/PicGo)，由于我想要以网页的方式进行管理，所以就自己写了一个小站点，可以访问github查看我的[代码](https://github.com/rimdl/GitPic)。
- 可以将其部署在GitHub pages，gitee pages，cloudflare pages等平台。
******
> 配置
- 部署完成打开后默认是如下界面![GitPic](https://raw.gitmirror.com/xinsi-tecool/mypic/main/7c601f13-5890-4e9d-95d3-30fc8e48f96f.png)
- 配置内容：
    - 在`仓库`位置填入你的仓库信息，例如，本项目的仓库地址是[https://github.com/rimdl/GitPic](https://github.com/rimdl/GitPic)，此处填入`rimdl/GitPic`即可。
    - `Token`处填写上面提到的在github获取的`token`。
    - `cdn`处填写用于加速github静态资源的cdn链接，例如：`https://cdn.jsdelivr.net/gh/`，默认的github链接在国内访问体验非常不好，所以加入cdn加速会好很多。
    - 配置完成后点击`保存`，将会在浏览器本地保存以上信息，例如使用chrome浏览器可以通过以下步骤查看到：`F12`->`应用`->`本地存储空间`->`本项目域名`。
    - 所以，由于这些信息都保存在浏览器本地，会有丢失的风险，获取到的`token`只会在github显示一次，丢失后只能重新获取，因此建议将以上配置信息单独备份到一个不会丢失的地方。
******
> 上传图片
- 成功配置后，将会显示如下界面![上传图片](https://raw.gitmirror.com/xinsi-tecool/mypic/main/3592165d-1dd9-4a2a-89c5-d94452f16b33.png)
- 右侧上传区域，拖动或者点击文件到此即可上传。
- 下方左侧显示你的GitHub账户信息(用户名和邮箱)，**注意：邮箱如果无法获取的，请到github进行配置，否则某些功能将会受限**
- 邮箱配置（正常获取到邮箱的请跳过此步骤）
    - 打开[链接](https://github.com/settings/emails)，取消勾选`Keep my email addresses private`![邮箱配置](https://raw.gitmirror.com/xinsi-tecool/mypic/main/d7f77bd1-333a-4fa8-85d0-c8b29b8560a5.png)
    - 再打开[链接](https://github.com/settings/profile)，设置`Public email`，选择你的邮箱即可![邮箱配置](https://raw.gitmirror.com/xinsi-tecool/mypic/main/ffba32c7-aabe-4f2a-85fc-4cbab4474b8a.png)
- 图片上传成功后，会在下方显示，点击`复制`按钮即可将链接复制到剪贴板，然后到你需要使用该图片的地方粘贴即可。（注意：上传的文件将会以`UUID`的形式重新命名。在设置了`cdn`的情况下，图片链接将会修改为`cdn`加速后的链接。）![上传图片](https://raw.gitmirror.com/xinsi-tecool/mypic/main/89d07d0f-5837-419f-8ff5-0e0dd18d04f6.png)
******
> 管理图片
- 在本程序下方会展示仓库中所包含的所有图片，图中的`获取当前仓库文件`与`刷新`两个按钮功能相同，图片在上传成功后并不能立刻显示在此处，所以添加此功能按钮用于刷新（注意：上传成功后请等待一定的时间，再点击刷新。）图中关于填充方式的几个按钮的功能请参考[Image 图片](https://element-plus.org/zh-CN/component/image.html)![图片管理](https://raw.gitmirror.com/xinsi-tecool/mypic/main/e99ea3fa-f9f1-454b-a1cb-a33c6768bc5a.png)。
- 点击图片可查看大图，点击复制链接可复制当前图片的链接，点击删除可删除此图片![图片管理](https://raw.gitmirror.com/xinsi-tecool/mypic/main/a7a19bdf-b630-454b-8a41-d536432c99c3.png)
******
# 结束
- 以上就是本次搭建图床的全部过程。