---
layout: post
title:  "code-prettifyがgithubに移行し進化していたので対応した"
date:   2016-06-15 23:16:00.000 09:00
categories: site-management
---

code-prettifyはGoogle謹製シンタックスハイライターです。 

以前は以下の構成が必要でした。 

```html
<!-- prettify -->
<style type='text/css'>
@import "http://google-code-prettify.googlecode.com/svn/trunk/src/prettify.css";
</style> 
<script src='http://google-code-prettify.googlecode.com/svn/trunk/src/prettify.js' type='text/javascript'></script>
<script type='text/javascript'>
function prettify() {
 prettyPrint();
}
if (window.addEventListener) {
  window.addEventListener("load", prettify, false);
} else if (window.attachEvent) {
  window.attachEvent("onload", prettify);
} else {
  window.onload = prettify;
}</script> 
<!-- prettify -->
```

進化後はたった一行で済みます。すごいですね。 

```html
<script src="https://cdn.rawgit.com/google/code-prettify/master/loader/run_prettify.js"></script>
```
