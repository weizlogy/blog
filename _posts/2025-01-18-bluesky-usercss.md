---
layout: post
title:  "WindowsでBluesky公式webページをUserCSSでキレイに見せる"
date:   2025-01-18 23:10:00 09:00
categories: software
---

<!--more-->

## 概要

WindowsでBluesky公式webページを対象に、Google ChromeのUser JavaScript and CSSアドオンでフォント調整を行い、キレイに見せます。

なぜプロポーショナルフォントなのかUI担当に問い詰めたい。

## 紹介

### 適用前

[![](https://www.dropbox.com/scl/fi/z5greztfrntsrys4k5g27/bluesky-stylish-before.png?dl=1)](https://www.dropbox.com/scl/fi/z5greztfrntsrys4k5g27/bluesky-stylish-before.png?dl=0)

### 適用後

[![](https://www.dropbox.com/scl/fi/b3c6j29psyuvyxwyhalah/bluesky-stylish-after.png?dl=1)](https://www.dropbox.com/scl/fi/b3c6j29psyuvyxwyhalah/bluesky-stylish-after.png?dl=0)

## 導入

### User JavaScript and CSSインストール

Google Chromeの機能拡張でUser JavaScript and CSSをインストールします。

### User JavaScript and CSSでスタイル作成

#### コード

```css
@import url('https://fonts.googleapis.com/css2?family=Noto+Sans+JP:wght@100..900&display=swap');
@import url('https://fonts.googleapis.com/css2?family=Noto+Sans+Mono:wght@100..900&display=swap');

// テキスト全体
.css-146c3p1
, .css-146c3p1 > a {
  font-family: "Noto Sans Mono", "Noto Sans JP" !important;
  font-weight: normal !important;
  font-size: 12px !important;
}

// プロフィールのユーザー名
div[data-testid="profileHeaderDisplayName"] {
	font-family: "Noto Sans Mono", "Noto Sans JP" !important;
  font-weight: bold !important;
  font-size: 20px !important;
}

// プロフィールのフォロー数あたり
.css-175oi2r .r-12vffkv > div
, .css-175oi2r .r-12vffkv > div > span {
  font-family: "Noto Sans Mono", "Noto Sans JP" !important;
  font-weight: bold !important;
  font-size: 14px !important;
}

// 投稿ユーザー名
a > .css-1jxf684 {
  font-family: "Noto Sans Mono", "Noto Sans JP" !important;
  font-weight: bold !important;
  font-size: 14px !important;
}

// 投稿リンク
button > .css-1jxf684,
.css-175oi2r .r-xoduu5 > .css-1jxf684 {
  font-family: "Noto Sans Mono", "Noto Sans JP" !important;
  font-weight: bold !important;
  font-size: 12px !important;
}

// 投稿エディター
div[data-testid="composePostView"] > div > div > div > div > div > div > div {
  font-family: "Noto Sans Mono", "Noto Sans JP" !important;
  font-weight: normal !important;
  font-size: 12px !important;
}
```

font-sizeは好みに応じて適宜調整してください。

#### 適用先

次で始まるURL　https://bsky.app/*

#### 保存！！！

## 更新履歴

### v1.0.0

#### 新規作成
