---
title: "Hugo: 在 Github 上部署 blog"
date: 2018-03-21T00:15:10+09:00
draft: false
tags: ["hugo", "blog"]
categories: ["hugo"]
---

# 关于 GitHub Pages

GitHub Pages 有两种页面：User Pages 和 Project Pages，这里讲一下如何将 Hugo 部署在 User Pages 上。

关于 User Pages 和 Project Pages 请参照 [Github](https://help.github.com/articles/user-organization-and-project-pages/#user--organization-pages)。

# 部署步骤:

1. 首先在 GitHub 上创建`<YOUR-PROJECT>`项目（例：`blog`），与 Hugo 相关的文件要放在这个项目里
2. 在 GitHub 上创建`<USERNAME>.github.io`项目，这个项目用来放编译后的静态网页（public下的内容）
3. `git clone <YOUR-PROJECT-URL> && cd <YOUR-PROJECT>`
4. （可选）确保 Hugo 可以在本地运行。`hugo server`然后在 http://localhost:1313 上查看
5. （可选）确认后停止 hugo (Ctrl + C)，并清除 hugo 下的 public 文件夹`rm -rf public`
6. `git submodule add -b master git@github.com:<USERNAME>/<USERNAME>.github.io.git public` 在 public 下创建子模块并关联到`<USERNAME>.github.io.git`项目中

# 部署自动化

将以下代码保存到`deploy.sh`放入 hugo 目录下：

```
#!/bin/bash

echo -e "\033[0;32mDeploying updates to GitHub...\033[0m"

# Build the project.
hugo # if using a theme, replace with `hugo -t <YOURTHEME>`

# Go To Public folder
cd public
# Add changes to git.
git add .

# Commit changes.
msg="rebuilding site `date`"
if [ $# -eq 1 ]
  then msg="$1"
fi
git commit -m "$msg"

# Push source and build repos.
git push origin master

# Come Back up to the Project Root
cd ..
```

使用`./deploy.sh "Your optional commit message"`实现提交和推送 public 下的静态网页

# 参考

https://gohugo.io/hosting-and-deployment/hosting-on-github/
