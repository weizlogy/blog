---
layout: post
title:  "表示されないマップを表示するアドオン"
date:   2018-01-17 22:13:20 09:00
categories: tos-addon
---

## download.

[[v1.0.1] showhiddenmap.ipf](https://github.com/weizlogy/tos/releases/download/showhiddenmap/showhiddenmap-v1.0.1.ipf)

## install.

[README.md](https://github.com/weizlogy/tos/blob/master/README.md)

## introduction.

## settings.

## descriptions.

### v1.0.1

#### マップ更新ロジック修正

FPS_UPDATE->RunUpdateScript(0.2)に変更することでスムーズ具合が向上しました。（ぬるぬるとは言ってない）

### v1.0.0

#### 新規作成

アドオンがロードされると、（ミニ）マップが表示されないマップで（ミニ）マップが表示されるようになります。
とある事情で、通常マップに比べるとちょっとマップ位置更新がスムーズではありませんが...

というのも、MAP_CHARACTER_UPDATEのイベントが発生しないっぽいので、FPS_UPDATEで代用しているためだったり。
