---
layout: post
title:  "Monodevelopで埋め込みリソースを使う"
date:   2016-07-31 16:11:00.000 09:00
categories: system-dev
---

<!--more-->

ソリューションエクスプローラーで対象のファイルを右クリックします。

「ビルドアクション > EmbeddedResource」を選択します。以上です。

プログラムからのアクセスで必要なリソースIDは、デフォルトネームスペース＋ファイル名となります。
リソースIDはプロパティビューで変更可能です。

使い方は以下の通りです。

```C#
using (var stream = new System.IO.StreamReader(System.Reflection.Assembly.GetExecutingAssembly().GetManifestResourceStream("[ResourceID]"), true)) {
    ...
}
```
