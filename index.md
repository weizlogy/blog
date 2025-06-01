---
# Feel free to add content and custom Front Matter to this file.
# To modify the layout, see https://jekyllrb.com/docs/themes/#overriding-theme-defaults

layout: default # ページのレイアウトを指定
description: "Weiβlogyのトップページへようこそ！最新の技術情報、役立つTips、そして管理人の日々のつぶやきなど、盛りだくさんでお届けします。気になる記事を見つけて、ゆっくり楽しんでいってくださいね！" # トップページ専用のmeta description
---

## About

{{ site.description }} <!-- サイト全体の概要 -->

ここでは、管理人が開発しているWindows向けのオリジナルソフトや、
その開発過程で遭遇した「うわっ、ハマった！」っていう技術的な躓きポイント、
そして「こうやって解決したよ！」っていう実践的な情報を中心に、
同じようなことで困ってる誰かのヒントになれば。

自己紹介的なページは特に用意してないんだけど、こんな感じで活動しています！

- [Bluesky](https://bsky.app/profile/weizlogy.com){:target="_blank"}
- [CodePen](https://codepen.io/weizlogy/full/LgjJYb){:target="_blank"}
- [Misskey](https://misskey.io/@twilightalpaca){:target="_blank"}
- [X(Twitter)](https://x.com/twilightalpaca){:target="_blank"}

## Tree of Savior Addons

- [自作したTree of Savior用のアドオン]({% link _pages/tos-addons.md %})
  > 自作したTree of Savior用アドオンの一覧です。各アドオンの機能説明、ダウンロードリンク、およびREADMEへのリンクを掲載しています。
- [自作中に必要になったTree of Savior用のアドオンの知識など]({% link _pages/tos-addon-develop.md %})
  > Tree of Saviorのアドオン開発者向けガイドです。

## 自作ソフトウェア

- [開発中の自作ソフトウェア]({% link _pages/softwares.md %})
  > 現在開発中のWindows向けオリジナルソフトウェアの情報を掲載しています。
- [開発が終了した自作ソフトウェア]({% link _pages/softwares-eol.md %})
  > 過去に開発し、現在は開発を終了したWindows向けオリジナルソフトウェアのアーカイブです。

## Updated Posts
{% assign updated_posts = site.posts | where_exp: 'post', 'post.last_modified_at != nil' | sort: 'last_modified_at' | reverse %} <!-- 更新日時でソート -->
{% if updated_posts.size > 0 %}
  {% for post in updated_posts limit: 5 offset: 0 %}
  - [{{ post.title }}]({{ post.url }})
    > {{ post.date | date: "%Y/%m/%d" }} {% if post.last_modified_at %} ~ {{ post.last_modified_at | date: "%Y/%m/%d" }}{% endif %}
    {% if post.excerpt %}
      <div class="post-excerpt">
        {{ post.excerpt | strip_html | truncatewords: 30 }}
      </div> <!-- HTMLタグを除去し、30単語に丸める -->
      <p><a href="{{ post.url }}" class="read-more">続きを読む &raquo;</a></p>
    {% endif %}
  {% endfor %}
{% endif %}

## Latest Posts

{% assign sorted_posts = site.posts | sort: 'date' | reverse %}
{% if sorted_posts.size > 0 %}
  {% for post in sorted_posts offset: 0 %}
  - [{{ post.title }}]({{ post.url }})
    > {{ post.date | date: "%Y/%m/%d" }}
    {% if post.excerpt %}
    <div class="post-excerpt">
      {{ post.excerpt | strip_html | truncatewords: 30 }}
    </div> <!-- こちらも30単語に統一 -->
    <p><a href="{{ post.url }}" class="read-more">続きを読む &raquo;</a></p>
    {% endif %}
  {% endfor %}
{% endif %}