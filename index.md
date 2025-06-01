---
# Feel free to add content and custom Front Matter to this file.
# To modify the layout, see https://jekyllrb.com/docs/themes/#overriding-theme-defaults

layout: default # ページのレイアウトを指定
description: "Weiβlogyのトップページへようこそ！最新の技術情報、役立つTips、そして管理人の日々のつぶやきなど、盛りだくさんでお届けします。気になる記事を見つけて、ゆっくり楽しんでいってくださいね！" # トップページ専用のmeta description
---

{{ site.description }} <!-- サイト全体の概要 -->
ここでは、管理人が開発しているWindows向けのオリジナルソフトや、
その開発過程で遭遇した「うわっ、ハマった！」っていう技術的な躓きポイント、
そして「こうやって解決したよ！」っていう実践的な情報を中心に発信してる（予定）よ。
同じようなことで困ってる誰かのヒントになったら嬉しいな。ゆっくりしていってね！

## About

自己紹介的なページは特に用意してないんだけど、こんな感じで活動してるよ！

- [Bluesky](https://bsky.app/profile/weizlogy.com){:target="_blank"}
- [CodePen](https://codepen.io/weizlogy/full/LgjJYb){:target="_blank"}
- [Misskey](https://misskey.io/@twilightalpaca){:target="_blank"}
- [X(Twitter)](https://x.com/twilightalpaca){:target="_blank"}

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
  {% for post in sorted_posts limit: 5 offset: 0 %}
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