---
layout: post
title:  "BeanUtils.describe()で配列を扱いたい"
date:   2011-09-10 00:03:00.000 09:00
categories: system-dev
---

<!--more-->

題名の通り、BeanUtils.describe()で配列を扱いたいのです。主にStringの配列。

BeanUtils.describe()を使うと、クラスのフィールドをMapに変換してくれますが「文字列として表現可能な形式のもの」に限ります。

Stringの配列については配列の先頭を出力し、残りは切り捨てられます。

※{"a", "b", "c"}という配列がある場合、"a"以外の値が切り捨てられます。

これは、BeanUtilsBeanの仕様となっております。

ただし、「commons beanUtils 1.8.0」以降は以下の回避策があります。

```java
BeanUtilsBean.setInstance(new BeanUtilsBean2());
ArrayConverter converter = new ArrayConverter(String[].class, new StringConverter(), 0);
// OnlyFirstToStringがtrueの場合、配列の先頭だけ使用します
converter.setOnlyFirstToString(false);
ConvertUtils.register(converter, String[].class);
```

上記処理はインスタンスを共有するため、他に影響がある場合は後処理も必要です。

```java
ConvertUtils.deregister(String[].class);
BeanUtilsBean.setInstance(new BeanUtilsBean());
```

Converterインターフェースを実装したクラスを作成し、ConvertUtilsにregistすると、独自の変換も可能です。
