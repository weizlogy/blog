---
layout: post
title:  "Webアプリケーションでサーバー上の画像ファイルをIMGタグに動的出力する"
date:   2014-04-15 13:15:00.002 09:00
description: "Webアプリケーションでサーバー上の画像ファイルをIMGタグに動的に出力する方法を解説。JSPとサーブレットを用いた実装例や、データベースのBlob型画像の扱い、レスポンスヘッダー設定の注意点などを紹介します。"
categories: system-dev
---

Webアプリケーションでサーバー上の画像ファイルをIMGタグに動的に出力する方法は、開発でよく遭遇するシナリオの一つだよね。この記事では、JSPとサーブレットを使って、サーバーに保存されている画像ファイルをブラウザに表示する基本的な仕組みと、その実装例をステップバイステップで見ていくよ。データベースにBlob型で保存された画像を読み込む場合も、基本的な考え方は同じだから応用が利くはず！

<!--more-->

img タグにサーブレットの URL を埋め込んで、画面描画時に呼び出します。
呼び出した先では画像をバイナリ形式で読み込んで画面に出力します。

データベースに Blob 型で保存した画像の読み込みも、ロジックは同じです。

JSPでは...

```jsp
<img src="xxx.do" />
```

サーバーサイドでは...

```java
/** xxx.do から呼び出される Servlet */
protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
  // ファイルパスはどこからか入手する
  String file = "\\server\image\sample.jpg";
  if (file == null || "".equals(file)) {
    return;
  }
  try {
    // 画像を読み込む
    byte[] image = Files.readAllBytes(Paths.get(file));
　　  // レスポンスヘッダーを設定する
    response.setContentType("image/" + file.substring(file.lastIndexOf(".")));
    response.setContentLength(image.length);
    // servlet specification 3.1 によると OutputStream は
    // Servlet 終了時にクローズされる
    // 従って、ここではクローズしない
    // むしろ、ここでクローズすると二重解放になる可能性があるのでは？
    response.getOutputStream().write(image);
  } catch (IOException e) {
    // ログ出力など
    throw e;
  }
}

protected void doPost(... 以下略
```
