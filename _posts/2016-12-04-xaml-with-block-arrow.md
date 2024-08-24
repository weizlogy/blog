---
layout: post
title:  "XAMLでブロック矢印を描画する"
date:   2016-12-04 22:45:00.001 09:00
categories: system-dev
---

## ブロック矢印完成図

[![](https://2.bp.blogspot.com/-QPmVEzpBOBo/WEQVzFGr4lI/AAAAAAAACdY/1nNprsKOYfsPBfK8hDGLXTx06mNUabT0ACLcB/s320/block_arrow.png)](https://2.bp.blogspot.com/-QPmVEzpBOBo/WEQVzFGr4lI/AAAAAAAACdY/1nNprsKOYfsPBfK8hDGLXTx06mNUabT0ACLcB/s1600/block_arrow.png)

## コード

```xml
  <Path Stroke="Black" StrokeThickness="2" Fill="Gray" Data="M 100 100 H 200 V 90 L 230 115 L 200 140 V 130 H 100 V 100 Z" Margin="-30,-30,0,0" />
```

## 解説

Pathを使って目標の位置付近に描画、Marginで微調整します。 

[https://msdn.microsoft.com/en-us/library/ms752293%28v=vs.110%29.aspx](https://msdn.microsoft.com/en-us/library/ms752293%28v=vs.110%29.aspx)を読めば分かりますが簡単です。
一筆書きの要領で、矢印の左上から時計回りに線を引いています。

「M 100 100」は「X=100,Y=100に移動」します。 

「H 200」は「現在位置からX=200まで描線」します。 

「V 90」は「現在位置からY=90まで描線」します。 

「L 230 115」は「現在位置からX=230,Y=115まで描線」します。 

以下繰り返しの上、 「Z」は「描線の範囲を閉鎖」します。 

座標の算出には、描画開始位置、シャフトの幅と高さ、アローヘッドの出代と角度を決めます。 
今回は、描画開始位置=100,100、シャフトの幅=100、高さ=30、アローヘッドの出代=10、角度=60にしました。 

[![](https://1.bp.blogspot.com/-GYh_fEvUajg/WEQcFVO7iYI/AAAAAAAACdo/LHnxOMOol1kDZPx3IPGsuZgHBEPJX6uJACLcB/s1600/block_arrow_calc.png)](https://1.bp.blogspot.com/-GYh_fEvUajg/WEQcFVO7iYI/AAAAAAAACdo/LHnxOMOol1kDZPx3IPGsuZgHBEPJX6uJACLcB/s320/block_arrow_calc.png)

アローヘッドの頂点座標の算出は、頂点がシャフトの中央にあることと、三平方の定理を使えばきっちり出せます。
つまり、シャフトの幅は偶数が良いです。 
