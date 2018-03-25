---
author: "Weibin Luo"
title: "在 Mac 和 Python3 上安装 MeCab"
date: 2018-03-25T21:35:22+09:00
draft: false
tags:
- mecab
- 形態素解析
- nlp
- python
categories:
- nlp
- mecab
keywords:
- nlp
- mecab
thumbnailImage: http://res.cloudinary.com/luoweibinb/image/upload/v1521982846/hugo/python/python-logo.png
---

如何在 Mac 和 Python 上安装 MeCab。
<!--more-->

---

# Mac 安装步骤

从 GitHub 上 clone 并 make （注意指定编码为 `utf-8` 否则可能会有乱码）

```
git clone https://github.com/Amabel/mecab
cd mecab/mecab
./configure  --enable-utf8-only
make
make check
sudo make install
```

安装日语字典 （同样注意编码）

```
cd ../mecab-ipadic
./configure --with-charset=utf8
make
sudo make install
```

在终端启动 MeCab

```
$ mecab
MeCab はフリーソフトウェアです
MeCab   名詞,固有名詞,組織,*,*,*,*
は 助詞,係助詞,*,*,*,*,は,ハ,ワ
フリー   名詞,一般,*,*,*,*,フリー,フリー,フリー
ソフトウェア  名詞,一般,*,*,*,*,ソフトウェア,ソフトウェア,ソフトウェア
です  助動詞,*,*,*,特殊・デス,基本形,です,デス,デス
EOS
```

---

# 在 Python3 上安装

通过 pip 安装

```
pip install mecab-python3
```

使用时引入 MeCab 即可

{{< tabbed-codeblock "使用 MeCab" >}}
<!-- tab python -->
import sys
import MeCab
m = MeCab.Tagger ("-Ochasen")
print(m.parse ("今日もしないとね"))
<!-- endtab -->
{{< /tabbed-codeblock >}}

解析结果

```
今日  キョウ   今日  名詞-副詞可能     
も モ も 助詞-係助詞        
し シ する  動詞-自立   サ変・スル 未然形
ない  ナイ  ない  助動詞   特殊・ナイ 基本形
と ト と 助詞-接続助詞     
ね ネ ね 助詞-終助詞        
EOS
```

---

# 参考

https://qiita.com/grachro/items/4fbc9bf8174c5abb7bdd
