---
layout: post
title:  "cannot find source for binding with reference について"
description: "WPFで発生するエラー「Cannot find source for binding with reference 'RelativeSource FindAncestor, AncestorType='System.Windows.Controls.ItemsControl', AncestorLevel='1''」の原因と、XAMLのStyle定義におけるSetterプロパティでのAlignment定義との関連について解説します。"
keywords: "WPF, Binding, RelativeSource, FindAncestor, ItemsControl, Style, Setter, XAML, Data Error 4"
date:   2010-09-11 18:35:00.000 09:00
categories: system-dev
---

掲題の件について、検索キーワードにあがりましたので、簡単にまとめました。

WPFアプリケーション開発中に、ListBoxItemなどのStyle定義で `RelativeSource FindAncestor` を使用したBindingを設定すると、特定の条件下で「Cannot find source for binding with reference」というエラーに遭遇することがあります。この記事では、そのエラーメッセージと、考えられる原因について、具体的なXAMLコードを交えながら解説します。

<!--more-->

正式には、以下のErrorが発生しました。

System.Windows.Data Error: 4 : Cannot find source for binding with reference 'RelativeSource FindAncestor, AncestorType='System.Windows.Controls.ItemsControl', AncestorLevel='1''. BindingExpression:Path=HorizontalContentAlignment; DataItem=null; target element is 'ListBoxItem' (Name=''); target property is 'HorizontalContentAlignment' (type 'HorizontalAlignment')

System.Windows.Data Error: 4 : Cannot find source for binding with reference 'RelativeSource FindAncestor, AncestorType='System.Windows.Controls.ItemsControl', AncestorLevel='1''. BindingExpression:Path=VerticalContentAlignment; DataItem=null; target element is 'ListBoxItem' (Name=''); target property is 'VerticalContentAlignment' (type 'VerticalAlignment')

xamlのStyle定義のSetterプロパティでAlignmentを定義していると出るみたいです。
定義を外すとErrorは出ません。
みたいです。というのは、何故なのか理由が分からないためです。

以下、実際のコードの抜粋です。

```xml
<Style TargetType="{x:Type ListBoxItem}">
    <Setter Property="HorizontalContentAlignment" Value="{Binding Path=HorizontalContentAlignment, RelativeSource={RelativeSource AncestorType={x:Type ItemsControl}}}"/>
    <Setter Property="VerticalContentAlignment" Value="{Binding Path=VerticalContentAlignment, RelativeSource={RelativeSource AncestorType={x:Type ItemsControl}}}"/>
```
