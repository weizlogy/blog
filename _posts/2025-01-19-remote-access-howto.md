---
layout: post
title:  "Android端末でメインPCを外出先から操作するための備忘録"
date:   2025-01-19 18:00:00 09:00
categories: system-dev
---

![eyecatch](/assets/img/20250120eyecatch.webp)

## 概要

- Wake on LANの設定

- マジックパケット送信の仕掛け

- リモート接続用ソフト選定

## Wake on LANの設定

メインPCのマザーボードはASROCK B550M-HDVくん。以下の設定をUEFIから設定します。

```
Advanced > ACPI Configuration > PCIE Devices Power On > Enabled 
```

ネットワークアダプターのプロパティから、「Magic Packetでのみ、コンピューターのスタンバイ状態を解除できるようにする」に
チェックを入れます。

## マジックパケット送信の仕掛け

LAN内にDS215jというSynology製のNASがあるので、そこから送れるようにします。

- Synology NASにはMagic Packet送出コマンドがある

```
/usr/syno/sbin/synonet --wake （該当PCのMACアドレス : 区切り） eth0;
```

- タスクスケジューラーを使って任意のコマンドを実行する

タスクスケジューラーの設定について詳しく説明している[サイト](http://rikuntyudady.fc2.net/blog-entry-1375.html)があります。
助かります。

念の為、常時起動しているファブレット（死語）のSurfacePro2くんからも送れるようにします。

この[スクリプト](https://poga.jp/?p=182)が超便利だったので使わせていただきます。助かります。

## リモート接続用ソフト選定

### Chromeリモートデスクトップ
メリット
- 導入簡単
- スマホの小さい画面でも拡縮できて見やすい

デメリット
- 画質荒い、ラグい
- ホストが再起動すると繋げられない

### Parsec
メリット
- 導入簡単、画質良い、ラグ少なめ
- ホストが再起動しても繋げられる

デメリット
- Androidアプリはかなり使いにくい
キーボード表示すると、画面がキーボードに被らないように小さくなる→見にくい
- 画面の拡大縮小ができない→見にくい
- マウスカーソルは表示されない→操作しにくい

### Moonlight + Sunshine + Tailscale
メリット
- 画質良い
- 仮想ゲームパッド付いてくるの強い

デメリット
- 導入面倒、ラグい
- 外から繋げるのにVPN必須
- MoonlightのUIが古めかしい
- 画面の拡大縮小ができない
- ホストが再起動すると繋げられない

## まとめ

ラグが致命的なのでParsecしかないが、Androidアプリが使いにくくて辛い。改善に期待


