---
layout: post
title:  "hugo+github pagesからjekyll+github pagesに移行した"
date:   2024-08-25 14:00:00 09:00
categories: site-management
---

![eyecatch](/assets/img/20240825eyecatch.webp)

## hugoでサイト運営して困ったこと

### 毎回ビルドして成果物をPushしないといけない

めんどい。

## hugoで困ったことをjekyllで解決する

### 毎回ビルド

jekyllならmarkdownを書いてPushするだけ。

## 移行メモ

### テーマ

Github pages対応のテーマが[いろいろある](https://github.com/pages-themes)なかで、
[minimal](https://github.com/pages-themes/minimal)を選びました。

- 唯一の２ペイン構成
- スマホサイズだと左ペインが上にくる親切仕様
- ぱっと見シンプル

### jekyllを使う環境を構築

[Jekyll を使用して GitHub Pages サイトを作成する](https://docs.github.com/ja/pages/setting-up-a-github-pages-site-with-jekyll/creating-a-github-pages-site-with-jekyll)ページが用意されているので見ながらいけます。

jekyllはRuby製なので、gemの依存関係で死にそうだなって思っていたら...

#### bundle installでエラー発生

> error occurred while installing wdm (0.1.1), and Bundler cannot continue

これはGemfileの下記行を消せば通ります（が、それでいいのか？

> gem "wdm", "~> 0.1.1", :platforms => [:mingw, :x64_mingw, :mswin]
>> [参考](https://talk.jekyllrb.com/t/newbie-problems-with-wdm-errors/9233)

### jekyllのPostの規則

_postsに配置するmarkdownファイル名には命名規則があって、該当記事URLと関連します。

例えば、
> 2024-08-18-welcome-to-jekyll.md -> /2024/08/18/welcome-to-jekyll.html

markdownファイルのfront matterでcategory(categories)が指定されていると、
> (categories: jekyll update) -> jekyll/update/2024...

命名規則外のファイルは無視されます。
