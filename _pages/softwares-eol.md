---
layout: post
title:  "開発が終了した自作ソフトウェア"
date:   2016-12-18 16:55:00.000 09:00
last_modified_at: 2025-06-01 21:17:00 09:00
categories: software
description: "過去に開発し、現在は開発を終了したWindows向けオリジナルソフトウェアのアーカイブです。Tapete、RealtimeWhoisView、Schritt、CCCなどの機能やダウンロード情報を提供しています。"
---

過去に開発し、現在は開発を終了したWindows向けオリジナルソフトウェアのアーカイブです。
各ソフトウェアの機能やダウンロード情報などをまとめています。

<!--more-->

## Tapete - Windows spotlight画像抽出

Windows10のロック画面で使われるspotlight画像を厳選し、<ユーザーディレクトリ>\picture\Tapete フォルダにコピーします。

コピーは随時発生し、日次で最新状態にリセットします。 

壁紙のスライドショーで使用することを想定し、画像の厳選条件は、4KB以上かつ、
プライマリースクリーンの解像度以上としています。 

[Tapete.zip](https://www.dropbox.com/s/ur02vpusc9lb1kl/Tapete-1.0.0.zip?dl=0)

ダウンロードしたzipを解凍し、任意の場所に配置します。 

画面のフォルダパスをクリックすると、該当フォルダをエクスプローラーで開きます。 

最小化すると通知アイコン化します。アイコンをクリックすると復元します。 

自動起動はしないので、必要に応じてスタートアップに登録してください。 

コピー先は固定なので、ソフトリンクやジャンクションで任意の場所にコピーさせることもできます。 

<br>

## RealtimeWhoisView - グローバルIP＋国名表示ツール

グローバルIPとIPアドレスの所属する国名を右上にひっそり表示します。

[[v1.0.0] RealtimeWhoisView.exe](https://github.com/weizlogy/windows-apps/releases/download/RealtimeWhoisView-v1.0.0/RealtimeWhoisView.exe)

[![RealtimeWhoisViewのスクリーンショット](assets/img/softwares-eol/RealtimeWhoisView.png)](assets/img/softwares-eol/RealtimeWhoisView.png)

### v1.0.0

#### 新規作成

exeを実行するとグローバルIPと国名の表示されたウィンドウが右上に出現します。

一応ドラッグできますが、位置は覚えません。

VPN等、ネットワークが切り替わると自動的に更新します。

Proxyは通りません。

<br>

## Schritt - 論理ステップカウンター

Schrittは論理ステップカウンターです。 

従来のステップカウンターは物理行でカウントする方式が主流であるため、書き方により規模に差異が現れます。

Schrittは論理的に命令をカウントすることで、書き方による規模の差異を抑制することを目的に作られました。

SchrittはLinux(ubuntu)のMonoを使用し、C#で実装されているため、.Net Frameworkの恩恵を受けられる環境であれば動作します。

[Schritt](https://www.dropbox.com/s/8zf41fu9hwf15nk/Schritt-core.exe?dl=0)

### status.

| 言語 | 対応バージョン | 状況説明 |
|:---||:---||:---|
| C | 0.0.3-α |  |
| C++ |  | 順次対応予定 |
| C# | 0.0.1-α |  |
| Java | 0.0.2-α |  |
| VB |  | 順次対応予定 |
| JavaScript |  | 順次対応予定 |
| HTML |  | 順次対応予定 |
| CSS |  | 順次対応予定 |
| Ruby |  | 順次対応予定 |

.Net Framework 4.5以上が必要です。 

### v0.0.4-α

ディレクトリ再帰走査対応。

### v0.0.3-α

C言語対応。

### v0.0.2-α

Java言語対応。

### v0.0.1-α

新規作成。

実行体に対してコマンドライン引数でステップ数を計測するソースコードのパスまたはディレクトリを指定(複数可)します。
ディレクトリ指定の場合は、サブフォルダを再帰的に走査します。 

```bash
Schritt-core.exe test1.cs test2.cs
```

実行結果は標準出力にCSV形式で出力されます。 

```bash
filename,comment,step
test1.cs,10,20
test2.cs,0,5
```

### lisence.

SchrittはMITライセンスで提供します。

### limitations.

ソースコードの文字コードはBOM付きのUnicode、またはBOM無しのUTF-8に対応しています。 

<br>

## CCC - 色当てゲーム解析ツール

[KOLOR](http://kolor.moro.es/)、[The Color](http://game.ioxapp.com/eye-test/game.html)のような
色当てゲームを解析し正解を表示します。

[[v1.0.0] CCC.exe](https://github.com/weizlogy/windows-apps/releases/download/CCC-v1.0.0/CCC.exe)

[![CCCの動作GIF](assets/img/softwares-eol/ccc.gif)](assets/img/softwares-eol/ccc.gif)

### v1.0.0

#### 新規作成

exeを実行すると半透明ウィンドウが表示されます。
ウィンドウはドラッグ、リサイズ（右下）が可能で、色当て対象領域上に配置します。

Enterキーでキャプチャーし解析結果を表示します。
正解部分は透過されているため、そのままクリック等のアクションが可能です。
正解以外は正解の反転色で塗りつぶされます。

KOLORのように同色を探す場合はSameMode、The Colorのように異色を探す場合はDifferentModeを使用して下さい。

### EnterキーDown

キャプチャー結果をクリアします。

### EnterキーUp

現在のウィンドウ領域をキャプチャーし解析結果を表示します。

### DキーUp

モードをDifferentMode（黒枠）に切り替えます。

### SキーUp

モードをSameMode（赤枠）に切り替えます。

### TキーUp

一時的にウィンドウ領域全体を透過、透過解除を繰り返します。

### ESCキーUp

キャプチャー結果をクリアします。
