---
layout: post
title:  "bloggerで最終更新日時を表示する"
date:   2016-06-16 22:00:00.000 09:00
categories: site-management
categories: site-management
description: "Bloggerで記事の最終更新日時を表示する方法を紹介します。標準機能では取得できない最終更新日時を、JavaScriptとRSSフィードを利用して、個別記事ページと一覧ページの両方に対応させるカスタマイズ手順を解説。"
---

bloggerのテンプレートタグでは更新日時を取得できないので、[別の方法](http://blog2.k05.biz/2013/05/blogger-last-modified.html)を参考に、時刻追加、個別記事表示、一覧記事表示どちらも対応するようにしました。

Bloggerで記事の最終更新日時を表示する方法を紹介します。標準機能では取得できない最終更新日時を、JavaScriptとRSSフィードを利用して、個別記事ページと一覧ページの両方に対応させるカスタマイズ手順を解説。

<!--more-->

ポイントは最終更新日時を挿入する要素のID属性を各投稿記事固有のIDにすることです。

ここが固定だと、最も早く出現する要素1つにのみ更新日時が表示されてしまいます。

まず、最終更新日時を表示する領域を決めます。

[テンプレート] > [HTMLの編集] > [書式テンプレート] > [ウィジェットの移動] > [Blog1<ブログ投稿領域>]に移動します。

投稿領域近辺が良いと思いますので、&lt;b:includable id='post' var='post'&gt;...&lt;/b:includable&gt;を展開し、そこから好きな位置に決めます。
今回は、投稿日時の近辺にするため、&lt;span class='post-timestamp'&gt;と次の要素の間に以下の投稿に依存するコードを埋め込みます。 
```html
<!-- 最終更新日時 -->
<span expr:id='data:post.id' class='last-modified updated'></span>
<script type='text/javascript'>
  var id = "<data:post.id/>";
</script>
<script type='text/javascript'>
  var sHome = "<data:blog.homepageUrl/>";
  var sURL = "<data:post.url/>";
  sURL = sURL.replace(sHome, "")
  sURL = "/" + sURL;
  document.write(unescape("%3Cscript")+" src='"+sHome+"/atom.xml?redirect=false&amp;path="+sURL+"&amp;max-results=1&amp;alt=json-in-script&amp;callback=show_last_modified' type='text/javascript'"+unescape("%3E%3C/script%3E"));
</script>
```

各投稿のRSSからコールバックされる関数show_last_modifiedは投稿に依存せず不変のため、テンプレートの上部に(投稿の前に宣言できればどこでも良い)一度だけ宣言します。 

```html
<script type="text/javascript">// <![CDATA[
function show_last_modified(root) {
  var published = '';  
  var updated = '';
  for (var i = 0; i < root.feed.entry.length; i++) {
    published = root.feed.entry[i].published.$t;
    updated= root.feed.entry[i].updated.$t;
  }
  var dd_Y = updated.substring(0,4);
  var dd_M = updated.substring(5,7);
  var dd_D = updated.substring(8,10);
  var pp_Y = published.substring(0,4);
  var pp_M = published.substring(5,7);
  var pp_D = published.substring(8,10);
  if (dd_Y == pp_Y && dd_M == pp_M && dd_D == pp_D) {
    // 日付が同じときは出力しない
  } else {
    var dd_H = updated.substring(11,13);
    var dd_m = updated.substring(14,16);
    var dd_S = updated.substring(17,19);
    var updated_dd = "updated..."+ dd_Y + "/" + dd_M + "/" + dd_D + " " + dd_H + ":" + dd_m + ":" + dd_S;
    document.getElementById(id).innerHTML = updated_dd;
  }
  document.getElementById(id).title = updated;
} //]]>
</script>
```

保存して正しく動くか確認しましょう。 また、一覧記事表示ではRSSを記事数分ロードするため、一覧表示件数は控えめにしましょう。 
