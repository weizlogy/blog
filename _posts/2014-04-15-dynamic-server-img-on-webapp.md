---
layout: post
title:  "Webアプリケーションでサーバー上の画像ファイルをIMGタグに動的出力する"
date:   2014-04-15 13:15:00.002 09:00
categories: system-dev
---

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
