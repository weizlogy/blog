---
layout: post
title:  "strutsでJSPで動的に一覧表示した複数のForm値をServletで簡単に渡す"
date:   2011-05-15 01:21:00.001 09:00
categories: system-dev
---

strutsのActionFormには、「map-backed properties」「list-backed properties」という機能があります。

ActionFormにMapやListのフィールドと適切なアクセサーメソッドを用意することで、JSP-Servlet間のデータ送受信が動的に行われる仕組みです。

Formのフィールドをいくつも用意しなくていいところが、とても便利です。

基本的な使い方は、下記公式リンクが分かりやすくなっています。

[http://struts.apache.org/1.x/userGuide/building_controller.html#map_action_form_classes](http://struts.apache.org/1.x/userGuide/building_controller.html#map_action_form_classes)

今回の趣旨は、「map-backed properties」「list-backed properties」を併用することです。
検索結果等JSPで動的に一覧表示した複数のForm値を、簡単にActionで受け取ることができます。

struts1.3.10

java 1.6.0_18

以下のようなFormクラスを用意します。

```java
import org.apache.commons.beanutils.LazyDynaList;
import org.apache.commons.beanutils.LazyDynaMap;

public HogeForm extends ActionForm {

    private LazyDynaList values = new LazyDynaList(LazyDynaMap.class);

    public String getValue(int index) {
        return values.get(index);
    }

    public void setValue(int index, Object value) {
        return values.set(index, value);
    }

    public List<Map<String, String>> getValues() {
        // LazyDynaList, LazyDynaMapのままでは扱いにくいため、より一般的な型（List, Map）に変換します。
        List<Map<String, String>> convertValues = new ArrayList<Map<String, String>>();
        for (Object item : values) {
            convertValues.add(((LazyDynaMap) item).getMap());
        }
        return convertValues;
    }
}
```

JSPでは以下のように出力しておきます。
Formをsubmitすると、HogeFormのvaluesにList&lt;Map&gt;の形式で値が格納されています。

```jsp
<logic:iterate id="xxx" name="yyy" indexId="index">
<INPUT type="hidden" name="value[<%= index %>].aaa" value="<bean:write name="xxx" property="123" />" />
<INPUT type="hidden" name="value[<%= index %>].bbb" value="<bean:write name="xxx" property="456" />" />
<INPUT type="hidden" name="value[<%= index %>].ccc" value="<bean:write name="xxx" property="789" />" />
</logic:iterate>
```

Actionクラスでは以下のようにアクセス可能です。

```java
public ActionForward execute(
    ActionMapping mapping, ActionForm form, HttpServletRequest request, HttpServletResponse response) {

    HogeForm hogeForm = (HogeForm) form;
    List<Map<String, String>> values = hogeForm.getValues();
    System.out.println(values.get(0).get("aaa"));    // 123

    ...
}
```
