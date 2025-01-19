---
layout: post
title:  "WindowsでTwitter公式webページをUserCSSでキレイに見せる"
date:   2017-11-22 22:22:09 09:00
last_modified_at: 2025-01-19 21:57:00 09:00
categories: software
---

## 概要

WindowsでTwitter公式webページを対象に、Google ChromeのStylishアドオンでフォント調整を行い、キレイに見せます。

Macは元からキレイだから良いよね。。。

### 2024-08-24

あの、Stylishが改悪されすぎて終わっていたので、User JavaScript and CSSを使います。

## 紹介

### 適用前

[![](https://www.dropbox.com/s/xrln1g1xqgpz3hb/twitter-stylish-before.png?dl=1)](https://www.dropbox.com/s/xrln1g1xqgpz3hb/twitter-stylish-before.png?dl=0)

### 適用後

[![](https://www.dropbox.com/s/cjbk7trwo2drx46/twitter-stylish-after.png?dl=1)](https://www.dropbox.com/s/cjbk7trwo2drx46/twitter-stylish-after.png?dl=0)

## 導入

### User JavaScript and CSSインストール

Google Chromeの機能拡張でUser JavaScript and CSSをインストールします。

### User JavaScript and CSSでスタイル作成

#### コード

```css
@import url('https://fonts.googleapis.com/css2?family=Noto+Sans+JP:wght@100..900&display=swap');
@import url('https://fonts.googleapis.com/css2?family=Noto+Sans+Mono:wght@100..900&display=swap');

// テキスト全体
div[data-testid="tweetText"] .r-1tl8opc
, a[data-testid="tweet-text-show-more-link"]
, .r-18u37iz {
  font-family: "Noto Sans Mono", "Noto Sans JP" !important;
  font-weight: normal !important;
  font-size: 12px !important;
}

// 投稿ユーザー名
div[data-testid="User-Name"] .r-1tl8opc {
  font-family: "Noto Sans Mono", "Noto Sans JP" !important;
  font-weight: bold !important;
  font-size: 14px !important;
}

// 投稿エディター
div[data-testid="tweetTextarea_0"] > div > div > div > span > span
, .public-DraftEditorPlaceholder-inner {
  font-family: "Noto Sans Mono", "Noto Sans JP" !important;
  font-weight: normal !important;
  font-size: 12px !important;
}

// 広告除去
div[data-testid="placementTracking"] {
	display: none !important;
}
```

#### 適用先

次で始まるURL　https://x.com/*

#### 保存！！！

## 更新履歴

### v2.0.1

#### CSS修正

- 投稿エディターにCSSを追加適用しました。

- コメントで適用範囲を明示しました。

### v2.0.0

#### 機能拡張の変更とCSS修正

- 機能拡張はUser JavaScript and CSSにしました。

- 現行サイトに合わせてCSSを修正しました。

### v1.0.0

#### 新規作成

- Windows10で標準採用された游ゴシックをベースに英数字は'Helvetica Neue'を使います。

- 游ゴシックは、レギュラーサイズではフォントの線が細くなりボヤッとした印象を受けるため、ウェイトを掛けてくっきりはっきり見えるようにしました。
