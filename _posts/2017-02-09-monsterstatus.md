---
layout: post
title:  "ターゲット中のモンスターのステータスを表示するアドオン"
date:   2017-02-09 05:57:00.002 09:00
categories: tos-addon
---

## download.

[[v3.0.3] monsterstatus.ipf](https://github.com/weizlogy/tos/releases/download/monsterstatus/monsterstatus-v3.0.3.ipf)

[[v2.1.3] monsterstatus.ipf](https://github.com/weizlogy/tos/releases/download/monsterstatus/monsterstatus-v2.1.3.ipf)

## install.

[README.md](https://github.com/weizlogy/tos/blob/master/README.md)

## introduction.

<div class="video-container">
  <iframe src="https://www.youtube.com/embed/IjzyuRoAbQo" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</div>

## settings.

Nexon\TreeofSaviorJP\addons\monsterstatus\location.txt を作成します。

## descriptions.

### v3.0.3

#### ドロップアイテム表示制限対応

未鑑定アイテムは表示されないように修正しました。

#### フレーム位置保存対応

フレーム位置の保存/復元に対応しました。

### v3.0.2

#### 冒険日誌改変対応

[jtos] 冒険日誌改変に対応しました。

### v3.0.1

#### 冒険日誌改変対応

[itos] 冒険日誌改変に対応しました。

### v3.0.0

#### ダメージ表示対応

ステータスの代わりにダメージの期待値を表示します。

ダメージの期待値表示は物理、クリティカル、魔法の三種類です。
クリティカルの期待値には確率を表示します。

#### 経験値表示追加

キャラクター経験値とクラス経験値の表示を追加しました。

#### フレーム背景透過対応

フレームの透過率を上げて、表示を改善しました。

### v2.2.0

#### 移動種別表示追加

移動種別の表示を追加し、飛行しているか分かるようにしました。

#### 種族、属性表示追加

種族、属性の表示を追加しました。


### v2.1.3

#### ドロップアイテム表示制限対応

未鑑定アイテムは表示されないように修正しました。

#### フレーム位置保存対応

フレーム位置の保存/復元に対応しました。

### v2.1.2

#### 冒険日誌改変対応

[jtos] 冒険日誌改変に対応しました。

### v2.1.1

#### 冒険日誌改変対応

[itos] 冒険日誌改変に対応しました。

### v2.1.0

コンパクトなv2系のサポートを始めました。

### v2.0.0

#### 討伐数、ドロップアイテム名、アイテム収集率表示追加

冒険日誌から討伐数、ドロップアイテム名、アイテム収集率を取得、
表示する機能を追加しました。
また、ドロップアイテム名からアイテムツールチップが開けます。

#### 表示ステータス 、フォーマット調整

表示するステータスは現在のところ以下の通りです。

| 表示名 | 内容 |
|:---|:---|
|ATK|物理攻撃力(最大)
|MATK|魔法攻撃力(最大)
|DEF|物理防御力
|MDEF|魔法防御力

UIウィンドウをドラッグで移動できるようになりました。

設定はログイン中のみ有効です。

### v1.0.0

#### 新規作成

アドオンがロードされると、ターゲットしたモンスターのステータス（*1）が画面上部に表示されます。 

[*1] 表示するステータスは現在のところ以下の通りです。

| 表示名 | 内容 |
|:---|:---|
|ATK|物理攻撃力(最大)
|MATK|魔法攻撃力(最大)
|DEF|物理防御力
|MDEF|魔法防御力
|DR|回避率
|CDR|クリティカル回避率
|CATK|クリティカル攻撃力
|CDEF|クリティカル防御力