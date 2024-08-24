---
layout: post
title:  "JQueryUIのAutoCompleteを特定操作で強制選択する"
date:   2014-03-19 12:39:00.002 09:00
categories: system-dev
---

本来は blur 時に強制選択したかったのですが、候補確定時に AutoComplete の対象にフォーカスが当たる挙動を回避できなかったため、エンターキーで代用です。

```javascript
var obj = $('#autocomplete');
obj.on('keydown', function(e) {
　　// エンターキー以外を無視する
  if (e.which !== 13) {
    return;
  }
  // search メソッドの結果で候補が存在する場合、
  // autocompleteopen イベントが発行される
  // 候補が 0 件の場合は動作しない
  obj.on('autocompleteopen', function() {
    // 下矢印キーダウンイベントを作成し、候補の先頭を選択状態にする
    var keyDownEvent = $.Event('keydown');
    keyDownEvent.keyCode = $.ui.keyCode.DOWN;
    obj.trigger(keyDownEvent);
    // エンターキーダウンを作成し、選択状態の候補で確定する
    // →候補確定時のイベントが発火する
    keyDownEvent.keyCode = $.ui.keyCode.ENTER;
    obj.trigger(keyDownEvent);
    // 通常動作時は不要なイベントなので終了時に破棄しておく
    obj.off('autocompleteopen');
  });
  // 現在の入力値で検索する
  obj.autocomplete('search');
});
```
