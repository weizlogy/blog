---
layout: post
title:  "WindowsでTwitter公式webページをUserCSSでキレイに見せる"
date:   2017-11-22 22:22:09 09:00
last_modified_at: 2024-08-24 17:21:00 09:00
categories: software
---

## overviews.

WindowsでTwitter公式webページを対象に、Google ChromeのStylishアドオンでフォント調整を行い、キレイに見せます。

Macは元からキレイだから良いよね。。。

### 2024-08-24

あの、Stylishが改悪されすぎて終わっていたので、User JavaScript and CSSを使います。

## introduction.

### 適用前

[![](https://www.dropbox.com/s/xrln1g1xqgpz3hb/twitter-stylish-before.png?dl=1)](https://www.dropbox.com/s/xrln1g1xqgpz3hb/twitter-stylish-before.png?dl=0)

### 適用後

[![](https://www.dropbox.com/s/cjbk7trwo2drx46/twitter-stylish-after.png?dl=1)](https://www.dropbox.com/s/cjbk7trwo2drx46/twitter-stylish-after.png?dl=0)

## settings.

### User JavaScript and CSSインストール

Google Chromeの機能拡張でUser JavaScript and CSSをインストールします。

### User JavaScript and CSSでスタイル作成

#### コード

```css
@import url('https://fonts.googleapis.com/css2?family=Noto+Sans+JP:wght@100..900&display=swap');
@import url('https://fonts.googleapis.com/css2?family=Noto+Sans+Mono:wght@100..900&display=swap');

div[data-testid="User-Name"] .r-1tl8opc {
  font-family: "Noto Sans Mono", "Noto Sans JP" !important;
  font-weight: bold !important;
  font-size: 14px !important;
}

div[data-testid="tweetText"] .r-1tl8opc
, a[data-testid="tweet-text-show-more-link"]
, .r-18u37iz {
  font-family: "Noto Sans Mono", "Noto Sans JP" !important;
  font-weight: normal !important;
  font-size: 12px !important;
}
```

#### 適用先

次で始まるURL　https://x.com/*

#### 保存！！！

## descriptions.

### v2.0.0

#### 機能拡張の変更とCSS修正

- 機能拡張はUser JavaScript and CSSにしました。

- 現行サイトに合わせてCSSを修正しました。

### v1.0.0

#### 新規作成

Windows10で標準採用された游ゴシックをベースに英数字は'Helvetica Neue'を使います。

游ゴシックは、レギュラーサイズではフォントの線が細くなりボヤッとした印象を受けるため、ウェイトを掛けてくっきりはっきり見えるようにしました。
