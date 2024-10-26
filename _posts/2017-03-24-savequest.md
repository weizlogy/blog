---
layout: post
title:  "ワープ用クエスト誤完了防止アドオン"
date:   2017-03-24 05:28:54 09:00
categories: tos-addon
---

## download.

[[v1.2.5] savequest.ipf](https://github.com/weizlogy/tos/releases/download/savequest/savequest-v1.2.5.ipf)

## install.

[README.md](https://github.com/weizlogy/tos/blob/master/README.md)

## introduction.

[![](https://www.dropbox.com/s/3bz19fmp4wj9nha/savequest.png?dl=1)](https://www.dropbox.com/s/3bz19fmp4wj9nha/savequest.png?dl=0)

[![](https://www.dropbox.com/s/a80xpgyrfxba5ui/savequest-shortcut.png?dl=1)](https://www.dropbox.com/s/a80xpgyrfxba5ui/savequest-shortcut.png?dl=0)

## settings.

Nexon\TreeofSaviorJP\addons\savequest フォルダーを作成します。

### explanation.

savequestフォルダーには下記ファイルが自動的に生成され、
キャラクター毎にアドオンで使用する情報をログアウト後も保持するために使用します。

- quests_[cid].txt
- quests\_scl_[cid].txt

## descriptions.

### v1.2.5

#### 保存済みクエストを破棄しても保存状態が残る問題を修正

保存済みクエストを破棄しても保存状態が残るため、再受注してもNPCが消えたままでした。
保存済みクエストを破棄すると保存状態も破棄するように修正しました。

### v1.2.4

#### ショートカットフレームレイヤーレベル一括変更機能追加

ショートカットフレームの（ワープマーカー）右クリックメニューに「FlattenLayerLv」コマンドを追加しました。

### v1.2.3

#### ショートカットフレームレイヤーレベル動的調整機能追加

ショートカットフレーム上でマウスホイールをくるくるするとレイヤーレベルが動的に変わります。
現在値はチャット上に表示（ちょっと邪魔...）します。

レイヤーレベルはショートカットフレームを移動させた時に保存します（くるくるしただけでは保存しない！）ので、お忘れなきよう...

### v1.2.2

#### パーティー共有機能追加

クエストワープのショートカットフレームから右クリックメニューでパーティー共有/共有解除できるようになります。

#### ショートカットフレームレイヤーレベル調整

ショートカットフレームのレイヤーレベルを999 -> 199に変更しました。

worldmapのレイヤーレベルが200なので、それの下という感じです。

### v1.2.1

#### クエストワープショートカット位置固定機能追加

クエストワープのショートカットフレームを位置固定できるようにしました。

### v1.2.0

#### クエストワープショートカット作成機能追加

右クリックメニューにshortcutが追加されました。
本機能によりクエストワープのショートカットフレームを任意の場所に追加、削除できます。

### v1.1.1

#### 一部クエストが保存できない不具合の修正

おそらくメインクエはほとんど保存できなかったと思いますが、保存できるようになります。

### v1.1.0

#### クエスト欄操作機能追加

F5キーで表示するクエスト欄でも本アドオンの機能（右クリックメニュー）が使えるようになります。

#### ダイレクトクエストワープ機能追加

F5キーで表示するクエスト欄から直接クエストワープできるようになります。

ワープ可能なクエストの左上にワープアイコンが表示されるので、クリックしてください。

### v1.0.2

#### バグ対応

保存したクエスト情報がチーム毎に共有される問題を修正しました。

[issue #3](https://github.com/weizlogy/tos/issues/3)

本修正により、情報保存形式が変更され、クエスト保存状態が初期化されます。

お手数ですが、再チェックまたは、旧仕様情報（quests.txt）の内容をquests_[cid].txtにコピペしてください。

### v1.0.1

#### バグ対応

再ログイン時に前回の状態が保存されない問題を修正しました。

[issue #1](https://github.com/weizlogy/tos/issues/1)

### v1.0.0

#### 新規作成

アドオンがロードされると、任意の完了済みかつワープ可能なクエストのNPCを一時消去し、
ワープ直後の誤完了を防止できます。

## usage.

UI右のクエスト一覧にある条件を満たしたクエストのタイトルを右クリックすると、
メニュー（Save, Release, Shortcut, Cancel）が開きます。

### save & release.

saveを選択すると該当クエストのNPCは非表示となります。
また、save済みのクエストのワープアイコン直下に[saved.]の文字を表示します。

元に戻すにはreleaseを選択します。

### shortcut.

shortcutを選択すると画面右上近辺にワープアイコン＋マップ名の小さなフレームが出現します。

フレームはドラッグで好きな位置に移動できます。移動位置は自動保存され再ログイン時に復元します。

ワープアイコンにマウスカーソルを当てるとクエスト名をツールチップ表示します。

ワープアイコンを右クリックするとメニュー（(Un)Lock, (Un)Share, FlattenLayerLv, Remove, Cancel）が表示されます。

#### (Un)Lock

ショートカットフレームを位置固定、または固定解除します。

現在の位置固定状態に応じてトグル表示します。

#### (Un)Share

対象クエストをパーティー共有/解除します。

共有時はショートカットフレーム右端に共有アイコンが表示されます。
（クエスト一覧と同じやつです）

現在の共有状態に応じてトグル表示します。

#### FlattenLayerLv

メニューを出したショートカットフレームのレイヤーレベルを、すべてのショートカットフレームに展開します。

#### Remove

ショートカットフレームを削除します。

**クエスト完了、破棄に連動していないため、不要になったショートカットは手動で削除してください。**

## cautions.

念のため、アドオンは補助的な位置づけとし、
ワープ直後はNPCを選択しないよう留意してください。

一時消去したNPCは、release後、エリアチェンジで表示できます。