---
layout: post
title:  "アドオン作成～設置方法まとめ"
date:   2016-09-25 07:41:00.000 09:00
categories: tos-addon-dev
---

## 必要なもの

- [IPF Suite](http://www.tosbase.com/downloads/IPF_Suite.zip.html)
- [IPFUnpacker](https://github.com/r1emu/IPFUnpacker/releases)

## 作成手順 

### 1. アドオンの名前を決める 

"xxxaddonxxx"としてみます。全て小文字、記号なしが良いです。 

### 2. アドオンのGUIを作る 

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

### 3. アドオンのスクリプトを作る 

"xxxaddonxxx.lua"ファイルを作成します。アドオン名と関数名の"_ON_INIT"前までが、大文字で一致するようにします。 

```lua
function XXXADDONXXX_ON_INIT(addon, frame)
  -- 任意の初期化処理
end
```

### 4. アドオンをパッケージングする 

IPFSuite.exeを起動、上部メニューの[New]、[New Container]の順序でボタンを押します。

[New Container]ボタンを押した後、テキストボックスが出現するので、"addon_d.ipf"を入力します。

上部メニューの[Add Folder]ボタンを押します。フォルダ名はアドオン名と同じ"xxxaddonxxx"とします。

上部メニューの[Add]ボタンを押します。ファイル選択ダイアログが出現するので、先に作成したxmlとluaファイルを選択します。

上部メニューの[Save]ボタンを押します。保存するファイル名は"xxxaddonxxx.ipf"とします。

### 5. アドオンを暗号化する 

IPF Unpackerで暗号化します。"Done!"と表示されれば成功です。 

```bash
> ipf_unpack.exe xxxaddonxxx.ipf encrypt
[ipf_unpack.c:291 in main] Parsing IPF 'xxxaddonxxx.ipf' (encrypt) ...
[ipf_unpack.c:304 in main] Done!
```

## 設置手順 

### 1. アドオンファイル削除の対策をする 

このままではクライアント起動時に削除されるため、環境依存文字（📖とか⛄）をファイル名の先頭に付与します。 

### 2. アドオンファイルを設置する 

TreeofSaviorJP\patch、または、TreeofSaviorJP\data、に設置します。
