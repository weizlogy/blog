+++
title = "Windows10でTwitter公式webページをStylishでキレイに見せる"
publishdate = 2017-11-22T22:22:09+09:00
categories = [ "system" ]
version = "1.0.0"
+++

## overviews.

Windows10でTwitter公式webページを対象に、Google ChromeのStylishアドオンでフォント調整を行い、キレイに見せます。

Macは元からキレイだから良いよね。。。

## introduction.

### 適用前

[{{< amp-img src="https://www.dropbox.com/s/xrln1g1xqgpz3hb/twitter-stylish-before.png?dl=1" width="320" height="239" >}}](https://www.dropbox.com/s/xrln1g1xqgpz3hb/twitter-stylish-before.png?dl=1)

### 適用後

[{{< amp-img src="https://www.dropbox.com/s/cjbk7trwo2drx46/twitter-stylish-after.png?dl=1" width="320" height="239" >}}](https://www.dropbox.com/s/cjbk7trwo2drx46/twitter-stylish-after.png?dl=1)

## settings.

### Stylishインストール

Google Chromeの機能拡張でStylishをインストールします。

### Stylishでスタイル作成

#### コード

```css
body.ja, .TweetTextSize.TweetTextSize--normal, .ProfileHeaderCard-bio, .TweetTextSize .twitter-hashtag b, .TweetTextSize .twitter-atreply b, .with-icn b, .Trends .context-trend-item .trend-item-context, .Trends .context-trend-item .trend-item-stats, b, .new-tweets-bar, .ProfileCard-bio, .FollowStatus {
  font-family: "Helvetica Neue", "Verdana", "Yu Gothic", Meiryo, sans-serif;
  font-weight: 600;
}
```

#### 適用先

次で始まるURL　https://twitter.com

#### 保存！！！

## descriptions.

### v1.0.0

#### 新規作成

Windows10で標準採用された游ゴシックをベースに英数字は'Helvetica Neue'を使います。

游ゴシックは、レギュラーサイズではフォントの線が細くなりボヤッとした印象を受けるため、ウェイトを掛けてくっきりはっきり見えるようにしました。
