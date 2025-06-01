---
layout: post
title:  "strutsのFormFileからローカルファイルの絶対パスを取得"
date:   2011-04-24 01:02:00.001 09:00
categories: system-dev
---

<!--more-->

strutsのFormFileからローカルファイルの絶対パスを取得したいのです。
（取得しても無意味ですが）

eclipseのデバッガで参照すると、確かにprivate変数に絶対パスを持っていますが、アクセスするためのメソッドがありません。

リフレクションでアクセス可能です。

DiskFileItemを使用するために、「commons-fileupload.jar」が必要です。

struts1.3.10

java 1.6.0_18

```java
// formFileの実体は「org.apache.struts.upload.CommonsMultipartRequestHandler.CommonsFormFile」
Field f = formFile.getClass().getDeclaredField("fileItem");
f.setAccessible(true);
// fileItemは「org.apache.commons.fileupload.FileItem」を実装した「org.apache.commons.fileupload.disk.DiskFileItem」
DiskFileItem item = (DiskFileItem) f.get(formFile);
System.out.println(item.getName());
```
