---
layout: post
title:  "アドオンで自作スキンを使用する方法"
date:   2017-03-05 14:19:00.000 09:00
categories: tos-addon-dev
---

## ifpファイル内部構成

```
xxx.ipf
├───addon_d.ipf
│     └───xxx
│          ├───xxx.lua
│          └───xxx.xml
└───ui.ipf
      ├───baseskinset
      │    └───xxx.xml
      └───skin
           └───xxx.tga
```

## addon_d.ipf

[Tree Of Savior アドオン作成～設置方法まとめ]({% post_url 2016-09-25-create-addon %})
参照。

## ui.ipf

### baseskinset

自作スキンの読込とアドオン内部で使用するスキンの定義を行います。

xxx.xml

```xml
<?xml version="1.0" encoding="UTF-8"?>
<skinset name="Base">
  <imagelist category="ringcommand">
  <image name="image1" file="\skin\xxx.tga" imgrect="211 5 197 195"/>
  <image name="image2" file="\skin\xxx.tga" imgrect="417 5 197 195"/>
</imagelist>
</skinset>
```
#### name

アドオン内部で参照するスキン名。

オリジナルのスキン名と重複しないように気を付けます。

#### file

スキン読み込み元画像ファイルパス。

#### imgrect

スキン読み込み元画像ファイル内画像座標。

半角スペース区切りで四角形の左上と右下の頂点座標を指定します。
=> x, y, width, height

### skin

自作スキン画像ファイルを配置します。

## アドオン実装方法

### xml

```xml
<picture name="xxx" rect="0 0 70 30" margin="0 0 45 0" hittest="true" image="image1"/>
```

### lua

```lua
local pic = GET_CHILD(xxx, "xxx", "ui::CPicture");
pic:SetImage("image2");
```

## tgaファイル

画像ファイルの一つ。

[https://convertio.co/ja/png-tga/](https://convertio.co/ja/png-tga/)でtgaと各種画像拡張子の相互変換が可能です。
