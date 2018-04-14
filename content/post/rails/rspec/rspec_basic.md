---
author: "Weibin Luo"
title: "RSpec_basic"
date: 2018-04-13T21:57:16+09:00
draft: false
tags:
- rails
- rspec
- testing
categories:
- rails
- rspec
keywords:
- rails
- rspec
- testing
thumbnailImage:
thumbnailImagePosition: bottom
---

使用`RSpec`写测试模块
<!--more-->

---

# 安装 RSpec

在 Gemfile 中添加
```
group :development, :test do
  gem 'rspec-rails', '2.13.1'
end
```

使用`bundle`安装
```
$ bundle install
```

生成测试文件夹

```
$ rails g rspec:install
```

---

# 参考

[https://www.jianshu.com/p/1db9ee327357](https://www.jianshu.com/p/1db9ee327357)

[https://qiita.com/jnchito/items/42193d066bd61c740612](https://qiita.com/jnchito/items/42193d066bd61c740612)

{{< tabbed-codeblock "" >}}
<!-- tab java -->
<!-- endtab -->
{{< /tabbed-codeblock >}}
