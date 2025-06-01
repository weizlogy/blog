---
layout: post
title:  "自作中に必要になったTree of Savior用のアドオンの知識など"
description: "Tree of Savior (ToS) のアドオン開発に必要な知識、IPF SuiteやIPFUnpackerを使ったアドオンの作成・設置方法、iesファイルフォーマットの解説、自作スキンの使用方法などをまとめた開発者向けガイドです。"
date:   2016-12-31 17:29:00.001 09:00
last_modified_at: 2025-06-01 17:45:00 09:00
categories: tos-addon-dev
---

Tree of Savior (ToS) のアドオン開発に挑戦したいけど、何から手をつければいいか分からない…そんなあなたのために、アドオンの作成から設置、さらにはゲーム内ファイルの解析や自作スキンの導入方法まで、開発に必要な知識をまとめました。
この記事を読めば、あなたもToSアドオン開発者への第一歩を踏み出せるはずです。

<!--more-->

* TOC
{:toc}

## アドオン作成～設置方法まとめ

### 必要なもの

- [IPF Suite](http://www.tosbase.com/downloads/IPF_Suite.zip.html)
- [IPFUnpacker](https://github.com/r1emu/IPFUnpacker/releases)

### 作成手順 

#### 1. アドオンの名前を決める 

"xxxaddonxxx"としてみます。全て小文字、記号なしが良いです。 

#### 2. アドオンのGUIを作る 

"xxxaddonxxx.xml"ファイルを作成します。アドオン名とuiframe@nameの値が一致するようにします。 

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<uiframe name="xxxaddonxxx" x="10" y="10" width="100" height="100">
  <frame title="XXXaddonXXX" snapclient="true" snapframe="true"/>
  <option closebutton="false" hideable="false"/>
  <input hittest="true"/>
  <layer layerlevel="31" />
  <draw blend="100" drawtitlebar="false" drawframe="false"/>
  <controls>
    <richtext name="dummy" />
  </controls>
</uiframe>
```

#### 3. アドオンのスクリプトを作る 

"xxxaddonxxx.lua"ファイルを作成します。アドオン名と関数名の"_ON_INIT"前までが、大文字で一致するようにします。 

```lua
function XXXADDONXXX_ON_INIT(addon, frame)
  -- 任意の初期化処理
end
```

#### 4. アドオンをパッケージングする 

IPFSuite.exeを起動、上部メニューの[New]、[New Container]の順序でボタンを押します。

[New Container]ボタンを押した後、テキストボックスが出現するので、"addon_d.ipf"を入力します。

上部メニューの[Add Folder]ボタンを押します。フォルダ名はアドオン名と同じ"xxxaddonxxx"とします。

上部メニューの[Add]ボタンを押します。ファイル選択ダイアログが出現するので、先に作成したxmlとluaファイルを選択します。

上部メニューの[Save]ボタンを押します。保存するファイル名は"xxxaddonxxx.ipf"とします。

#### 5. アドオンを暗号化する 

IPF Unpackerで暗号化します。"Done!"と表示されれば成功です。 

```bash
> ipf_unpack.exe xxxaddonxxx.ipf encrypt
[ipf_unpack.c:291 in main] Parsing IPF 'xxxaddonxxx.ipf' (encrypt) ...
[ipf_unpack.c:304 in main] Done!
```

### 設置手順 

#### 1. アドオンファイル削除の対策をする 

このままではクライアント起動時に削除されるため、環境依存文字（📖とか⛄）をファイル名の先頭に付与します。 

#### 2. アドオンファイルを設置する 

TreeofSaviorJP\patch、または、TreeofSaviorJP\data、に設置します。

<br>

## iesファイルフォーマット解説

???は可変長です。

### Total block

```
 ------------------- ---------------------------- -------------------------
| Header [156 byte] | Cell Header [136 x N byte] | Row Data [??? x M byte] |
 ------------------- ---------------------------- -------------------------
```

N=列数。は、Header blockのCellCountで指定。 M=行数。は、Header blockのRowCountで指定。 

### Header block

```
 ---------------------- ------------------- ------------------------
| TableName [128 byte] | Reserve1 [4 byte] | OffsetOfData [4 byte]  |
 ---------------------- ------------------- ------------------------
 --------------------------- ------------------- -------------------
| OffsetOfResource [4 byte] | FileSize [4 byte] | Reserve2 [4 byte] |
 --------------------------- ------------------- -------------------
 ------------------- -------------------- --------------------------
| RowCount [2 byte] | CellCount [2 byte] | NumCellCount [2 byte]    |
 ------------------- -------------------- --------------------------
 ----------------------- -------------------------------------------
| StrCellCount [2 byte] | Reserve3 [2 byte] | --------------------- |
 ----------------------- -------------------------------------------
```

| | |
|:---|:---|
| TableName | IESテーブル名 |
| Reserve1 | 予約1 |
| OffsetOfData | Cell Header blockのサイズ |
| OffsetOfResource | Row Data blockのサイズ |
| FileSize | IESファイルサイズ |
| Reserve2 | 予約2 |
| RowCount | 行数 |
| CellCount | 列数 |
| NumCellCount | 数値列数 |
| StrCellCount | 文字列列数 |
| Reserve3 | 予約3 |

### Cell Header block

```
 ---------------- ------------------- ----------------------
| Name [64 byte] | Name2 [64 byte] | Type [2 byte] | ------ |
 ---------------- ------------------- ----------------------
 ------------------- ------------------- -------------------
| Reserve1 [2 byte] | Reserve2 [4 byte] | Position [2 byte] |
 ------------------- ------------------- -------------------
```

| | |
|:---|:---|
| Name | Cell名 |
| Name2 | Cell別名 |
| Type | 0：数値Cell、1,2：文字列Cell |
| Reserve1 | 予約1 |
| Reserve2 | 予約2 |
| Position | Type内Cell順序 |

Cell順は、Type昇順、Position昇順。 

### Row Data block

```
 ------------------- ---------------------- --------------------
| Option [??? byte] | Cell Data [??? byte] | Padding [??? byte] |
 ------------------- ---------------------- --------------------
```

Paddingは、文字列Cellの数だけ0x00が付与される。 

#### Option block

```
 ------------------- --------------- -----------------
| Reserve1 [4 byte] | Size [2 byte] | Name [??? byte] |
 ------------------- --------------- -----------------
```

| | |
|:---|:---|
| Reserve1 | 予約1 |
| Size | Nameのバイト長 |
| Name | Cellオプション名 |

#### Cell Data block

数値Cellの場合： 

```
 ----------------
| Value [4 byte] |
 ----------------
```

文字列Cellの場合： 

```
 --------------- ------------------
| Size [2 byte] | Value [??? byte] |
 --------------- ------------------
```

| | |
|:---|:---|
| Size | Nameのバイト長 |
| Name | 列データ |

<br>

### iesファイルをcsv形式のファイルに変換するソフト

Tree Of Savior (ToS) のゲームデータに含まれる `.ies` ファイル。これらは通常バイナリ形式で暗号化されており、直接内容を確認するのは困難です。
このツールは、そんな `.ies` ファイルを解析し、人間が読めるCSV形式に変換します。

### 概要

Tree Of Saviorのipfファイル内には拡張子がiesのファイルがあります。

Ipf Suiteでは中身を見ることができますが、extractしても実体はバイナリファイル（かつ、暗号化されている）で、
テキストエディタでもバイナリエディタでも見ても分かりません。

もちろん、grep検索で引き当てることもできません。

本ソフトは、iesファイルを解析し、可読性のあるcsvファイルを生成します。 

[IEStoCSV.zip](https://www.dropbox.com/s/61977sy5a2b1nwl/IEStoCSV.zip?dl=0)

ダウンロードしたzipを解凍し、任意の場所に配置します。 

### descriptions.

コンソールアプリケーションなので、コマンドプロンプトで操作します。 

```
IEStoCSV.exe <走査ディレクトリ>
```

サブフォルダを含む走査ディレクトリ配下のiesファイルに対して、対となるcsv形式のファイルを生成します。

走査ディレクトリ省略時は、本ソフトのある位置を対象とします。 

### caution.

iesファイル内に韓国語が含まれるので、Excelでは文字化けします。（ExcelはShiftJISですが、生成するcsvはUTF8なので）

本当は英訳を載せたいのですが、完全無料の翻訳APIがないもので。。。 需要があれば何とかしようと思います。 

### acknowledgment.

iesファイルフォーマットは、以下のソースコードを参考にさせて頂きました。 ありがとうございます。

https://github.com/r1emu/IPFUnpacker/blob/master 

## アドオンで自作スキンを使用する方法

### ifpファイル内部構成

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

### ui.ipf

#### baseskinset

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
##### name

アドオン内部で参照するスキン名。

オリジナルのスキン名と重複しないように気を付けます。

##### file

スキン読み込み元画像ファイルパス。

##### imgrect

スキン読み込み元画像ファイル内画像座標。

半角スペース区切りで四角形の左上と右下の頂点座標を指定します。
=> x, y, width, height

#### skin

自作スキン画像ファイルを配置します。

### アドオン実装方法

#### xml

```xml
<picture name="xxx" rect="0 0 70 30" margin="0 0 45 0" hittest="true" image="image1"/>
```

#### lua

```lua
local pic = GET_CHILD(xxx, "xxx", "ui::CPicture");
pic:SetImage("image2");
```

### tgaファイル

画像ファイルの一つ。

[https://convertio.co/ja/png-tga/](https://convertio.co/ja/png-tga/)でtgaと各種画像拡張子の相互変換が可能です。
