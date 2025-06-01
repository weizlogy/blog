---
layout: post
title:  "TSLで定義される全CipherSuiteの一覧"
date:   2017-01-31 21:59:00.001 09:00
categories: system-dev
---

<!--more-->

Cipher Suiteの説明はさて置き、一覧を見るために以下のコマンドを使用する例が多々見受けられます。 

```bash
$ openssl ciphers -v
```

これはopensslが対応するCipherSuiteの一覧であり、実際に存在するCipherSuiteの一覧とは異なります。 

実際に存在するCipherSuiteの一覧は、RFC5426によるとIANA管理とのことで、下記URLがマスターです。 

[http://www.iana.org/assignments/tls-parameters/tls-parameters.xhtml#tls-parameters-4](http://www.iana.org/assignments/tls-parameters/tls-parameters.xhtml#tls-parameters-4)
