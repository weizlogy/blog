---
layout: post
title:  "GUI操作で装備を保存/復元するアドオン"
date:   2018-04-11 23:48:28 09:00
categories: tos-addon
---

**ToSには**

## download.

[[v1.1.1] costumeplay.ipf](https://github.com/weizlogy/tos/releases/download/costumeplay/costumeplay-v1.1.1.ipf)

## install.

[README.md](https://github.com/weizlogy/tos/blob/master/README.md)

## introduction.

[![](https://www.dropbox.com/s/g7aaachkop2vswh/costumeplay.png?dl=1)](https://www.dropbox.com/s/g7aaachkop2vswh/costumeplay.png?dl=0)

## settings.

Nexon\TreeofSaviorJP\addons\costumeplay フォルダーを作成します。

## descriptions.

costumeplayフォルダーには下記ファイルが自動的に生成され、
キャラクター毎にアドオンで使用する情報をログアウト後も保持するために使用します。

- [cid]

### v1.1.1

#### 同一名称ブレスレットが正常に装備できない問題の修正

#### 装備名クリック時の動作修正

旧：一時的に復元状態を変更

新：永続的に復元状態を変更

### v1.1.0

#### ヘアカラー、称号追加

本バージョン以降に作成したデータは、ヘアカラーと称号を保存/復元できるようになります。

#### フレーム表示方法修正

インベントリを開くと追従して開かなくなりました。
閉じる場合は依然としてインベントリに追従します。

代わりに、インベントリアイコン右クリックメニューに[Open]が追加され、そこから開けます。
アドオンフレームが表示されるとインベントリが追従して開きます。

### v1.0.0

#### 新規作成

GUI操作で装備を保存/復元します。

## usage.

### 保存方法

- インベントリの左側にアドオンのフレームが表示されます。
- 名前を入力して[save]を押すと現在の装備を保存します。

### 復元方法

- 画面右下のインベントリアイコンを右クリックするとメニューが出現します。
- メニューには保存時に入力した名前がリストアップされるので任意のものを選択します。

### その他

- 見た目に影響しない防具やリングなどは初期状態で復元しない状態です。（装備名が灰色）
- アドオンフレームの装備名をクリックすると、永続的に復元状態を変更します。
