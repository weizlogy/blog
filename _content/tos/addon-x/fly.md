+++
publishdate = "2016-10-09T19:39:00.000+09:00"
title = "飛行アドオン"
categories = [ "tos-addon-x" ]
version = "1.2.0"
lastmod = "1900-01-01T00:00:00.000+09:00"
+++

## download.

[[v1.2.0] fly.ipf](https://www.dropbox.com/s/5gq04f1jpoju4na/fly.ipf?dl=0)

## install.

[README.md](https://github.com/weizlogy/tos/blob/master/README.md)

## introduction.

{{< amp-youtube width="480" height="270" videoid="Ad_LIzKk_no" >}}

## settings.

Nexon\TreeofSaviorJP\addons\fly\settings.txt を作成します。

以下の初期設定をコピペします。

```lua
fly.config = {
  pos = {x = 100, y = 100},
  jumpPower = 140,
  showButton = 0,
  cameraHeight = 50,
  withPet = 1
};
```

### explanation.

#### pos.

ボタンの座標指定です。

[showButton]が0の場合は無視されます。

#### jumpPower.

飛距離です。

100では弓に狙われます。 
150では通常攻撃が届きません。（wizでは140で届きます。）

#### showButton.

ボタン表示状態です。

1の場合のみ、飛行ON/OFFボタンを[pos]の座標に表示します。

#### cameraHeight.

飛行時のカメラ位置です。

飛距離によりますが、50～70あたりで自分の影が画面中央あたりに見え、歩行しやすいです。

0を指定すると、今まで通りの視点になります。

#### withPet.

ペット飛行有無です。

1を指定すると、ペットも一緒に飛行します。

## descriptions.

### v1.2.0

設定ファイルのフォーマット変更、cameraHeight、withPetオプションを実装しました。

### v1.1.0

設定[ボタン表示状態]を追加しました。

アドオンがロードされると、[ボタン表示状態]が1の場合のみ、[Fly]ボタンが表示されます。

ショートカットキーを追加しました。

ESCAPE+UP(上矢印)で飛行、飛行解除ができます。

### v1.0.0

新規作成。

アドオンがロードされると[Fly]ボタンが表示されます。

ボタンを押すと飛行状態、地上に降りるを繰り返します。

飛行状態でも地上の敵を攻撃できます。
飛行状態では地上の敵はこちらを近接攻撃できません。

実際は地上を歩行しているのでトラップには気をつけてください。 

飛行状態ではスキルが使用不可ですが、ノックバックを受けるとスキルが使用可能になりますので、わざとノックバックするようになっています。 

休息中に飛行すると、休息バフがついた状態で行動できます。
ただし、攻撃などの操作を行うと休息バフは解除されます。
