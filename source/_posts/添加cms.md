---

updated: '2024-01-22 14:28:17'  
filename: 添加cms  
date: '2024-01-22 14:28:12'  
categories: test  
tags:

*   '1'
*   '23'

---

# 为什么要添加这个“内容管理系统”

*   如果没有添加cms的话，正常写作博客时需要先在本地写好，再通过git push到github，这一过程较为繁琐，通过cms这种方式就可以实现在线形式的编写博客体验。123

# 开始

*   可参考[decapcms](https://decapcms.org/docs/add-to-your-site/)

## 项目配置

*   在hexo项目的`source`目录下创建`admin`目录，添加以下两个文件：

```plaintext
admin
 ├ index.html
 └ config.yml
```

*   `index.html`文件内容

```html
<!doctype html>
<html>
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <meta name="robots" content="noindex" />
  <title>Content Manager</title>
</head>
<body>
  <!-- Include the script that builds the page and powers Decap CMS -->
  <script src="https://unpkg.com/decap-cms@^3.0.0/dist/decap-cms.js"></script>
<!--上面的代码script是从unpkgCDN 加载的。如果有任何问题，jsDelivr可以用作替代来源。只需将其设置src为https://cdn.jsdelivr.net/npm/decap-cms@^3.0.0/dist/decap-cms.js-->
</body>
</html>
```

*   `config.yml`文件内容

```plaintext
backend:
  name: git-gateway
  branch: main # Branch to update (master by default)

# These lines should *not* be indented
media_folder: 'source/images' # Media files will be stored in the repo under source/images
public_folder: 'images' # The src attribute for uploaded media will begin with images

# This line should *not* be indented
publish_mode: editorial_workflow

collections:
  - name: 'Post' # Used in routes, e.g., /admin/collections/blog
    label: 'Post' # Used in the UI
    folder: 'source/_posts' # The path to the folder where the documents are stored
    create: true # Allow users to create new documents in this collection
    slug: '{{slug}}' # Filename template, e.g., YYYY-MM-DD-title.md
    fields: # The fields for each document, usually in front matter
      - {label: 'Title', name: 'title', widget: 'string'}
      - {label: 'Publish Date', name: 'date', widget: 'datetime'}
      - {label: 'Body', name: 'body', widget: 'markdown'}
```

*   完成以上文件的创建后，修改项目根目录的`_config.yml`文件，跳过对`source/admin`的渲染：

```plaintext
skip_render: admin/**
```

## netlify配置

打开[netlify](https://app.netlify.com)，点击自己部署的网站，点击`Site configuration`![pic1](https://raw.gitmirror.com/rimdl/pic/master/20240111200239.png)

点击`Build & Deploy`![pic2](https://raw.gitmirror.com/rimdl/pic/master/20240111200712.png)

点击`Post processing`![pic3](https://raw.gitmirror.com/rimdl/pic/master/20240111200835.png)

点击`Snippet Injection section`,`Add Snippet`，分别添加以下内容，`Script name`随意填写，以下内容填入`html`处：

> `Before</head>`

```html
<script src="https://identity.netlify.com/v1/netlify-identity-widget.js"></script>
```

> `Before</body>`

```html
<script>
  if (window.netlifyIdentity) {
    window.netlifyIdentity.on("init", user => {
      if (!user) {
        window.netlifyIdentity.on("login", () => {
          document.location.href = "/admin/";
        });
      }
    });
  }
</script>
```

![pic4](https://raw.gitmirror.com/rimdl/pic/master/20240111201028.png)

*   回到`Site configuration`处，点击`Identity`，再点击`Enable Identity`启用。
*   启用后点击`Registration`，再点击`Invite only`![pic5](https://raw.gitmirror.com/rimdl/pic/master/20240111201801.png)
*   `Registration preferences`处设置为`Invite only`，这样就只有你邀请的人才能编辑，防止被人恶意修改。
*   `~External providers~`~添加GitHub账号，可以启用使用github账户进行登录。~这样好像任何人使用GitHub登录都可以修改文章了。
*   完成以上步骤后，回到`Identity`处，分别点击`Services`，`Git Gateway`，`Enable Git Gateway`

## 访问

*   完成了以上操作后，在你的博客地址后面加入`/admin`，就可以进入到cms的页面了，通过GitHub账号或者你邀请的email账户进行登录后，即可进行在线的博客文章编写了。![pic6](https://raw.gitmirror.com/rimdl/pic/master/20240111202616.png)