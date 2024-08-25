---
layout: post
title:  schema.org構造化データBlogPosting対応 with JSON+LD in blogger
date:   2017-02-26 12:54:00.000 09:00
categories: site-management
---

bloggerのテンプレートで、以下のブログ投稿箇所を検索します。 

```xml
<b:loop values='data:posts' var='post'>
```

この直下に以下のスクリプトを挿入します。 

```xml
<!-- schema.org - BlogPosting. -->
<script type='application/ld+json'>
  {
    "@context": "http://schema.org",
    "@type": "BlogPosting",
    "headline": "<data:blog.url/>",
    "url": "<data:blog.pageTitle/>",
    "datePublished": "<data:post.timestampISO8601/>",
    "author": {
      "@type": "Person",
      "name": "<data:post.author/>"
    },
    "publisher": {
      "@type": "Organization",
      "name": "Weiβlogy",
      "logo": {
        "@type": "ImageObject",
        "url": "https://blog.weizlogy.com/favicon.ico"
      }
    },
    "dateModified": "<data:post.timestampISO8601/>",
    "mainEntityOfPage": "1",
    "image": {
      "@type": "ImageObject",
      "url": "https://blog.weizlogy.com/dummy.png",
      "width": "100",
      "height": "100"
    }
  }
</script>
```

publisher, imageは各自修正してください。 

datePublished, dateModifiedは今のところ同じ値になっています。

feedDataに情報はありますが、Javascriptを経由せず取得するのは難しそうです。 

本当はheaderタグ内に置きたかったのですが、data:postsが b:section class='main' id='main' 配下でないと
有効でないという仕様に阻まれました。。。 
