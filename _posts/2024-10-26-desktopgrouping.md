---
layout: post
title:  "Desktop Grouping - デスクトップ整理ソフト"
date:   2024-10-25 15:30:00 09:00
description: "デスクトップ上にシンプルな枠を設置してファイルを整理できる自作ソフト「Desktop Grouping」の概要、ダウンロード、導入方法を紹介します。"
last_modified_at: 2025-05-03 15:49:00 09:00
categories: software
---

デスクトップがファイルで散らかることはありませんか？この問題を解決するため、シンプルな枠でファイルを整理できる自作ソフトウェア「Desktop Grouping」を開発しました。この記事では、その概要や使用方法を紹介します。

<!--more-->

![Desktop Groupingのアイキャッチ画像。デスクトップ整理のイメージ。](/assets/img/20241026eyecatch.webp)

## 概要 (Overviews)

デスクトップ上にシンプルな枠を設置して、その枠にファイルをまとめて置くことができます。

## ダウンロード (Download)

[Desktop Grouping](https://github.com/weizlogy/DesktopGrouping/releases)

上記リリースページから、最新版のインストーラー (`Desktop.Grouping_X.X.X_installer.exe`) またはポータブル版 (`portable.7z`) をダウンロードしてください。
（バージョン番号は適宜最新のものに読み替えてください。）

## 導入・使い方 (Introduction)

[README](https://github.com/weizlogy/DesktopGrouping/blob/master/README.md)

詳しい使い方は、GitHubリポジトリにある README を確認してください。
基本的には、アプリケーションを起動するとデスクトップに半透明の枠が表示されます。そこに整理したいファイルやフォルダをドラッグ＆ドロップするだけで使用可能です。枠は複数作成でき、サイズや位置も自由に変更できます。

## 設定と起動 (Settings & Startup)

**インストーラー版の場合:**
ダウンロードした `Desktop.Grouping_X.X.X_installer.exe` を実行し、画面の指示に従ってインストールを進めてください。インストールが完了すると、スタートメニューなどから起動できるようになります。

**ポータブル版の場合:**
ダウンロードした `portable.7z` を、任意のフォルダに展開（解凍）するだけで準備は完了です。内部の `DesktopGrouping.exe` を実行することで使用できます。
もし、PC起動時に Desktop Grouping を自動起動したい場合は、この `DesktopGrouping.exe` のショートカットをWindowsのスタートアップフォルダに配置してください。
手順が不明な場合は、「Windows スタートアップ フォルダ」などのキーワードで検索すると、詳細な情報が見つかるでしょう。

## 更新履歴 (Changelog / Descriptions)

### v2.0.0

Rustで再実装したことにより、レスポンスが向上しました。
具体的には、アプリケーションの起動が速くなり、枠を移動する際の反応がスムーズになりました。以前よりも快適に使用できるようになりましたので、ぜひお試しください。

### v1.0.0

新規作成。
このバージョンはC# (WPF) で開発しました。初めてのデスクトップアプリケーション開発であり、試行錯誤を重ねて開発したバージョンです。
これがDesktop Groupingの最初のバージョンです。
