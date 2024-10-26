---
layout: post
title:  "Codeaywhere+Java+bazelでOpenWeatherMapのAPIを使用し現在の気象情報を取得する"
date:   2016-08-21 11:20:00.000 09:00
categories: system-dev
---

## OpenWeatherMapの使い方

[OpenWeatherMap](http://openweathermap.org/)は各種気象情報提供サービスです。

サインアップすれば無料で使える[API](http://openweathermap.org/api)も提供しています。

今回は現在のみなので、[Current weather data API](http://openweathermap.org/current)を使用します。
RESTサービスになっており、以下のURLで情報がJSON形式で取得できます。（{city name}は英語で）

```
http://api.openweathermap.org/data/2.5/weather?q={city name}&APPID={Your API Key}
```

JSON形式ではJavaで扱いにくいので、"mode=xml"パラメータでXML形式にします。 

```
http://api.openweathermap.org/data/2.5/weather?q={city name}&mode=xml&APPID={Your API Key}
```

気象情報は以下のように返却されます。（例は{city name}=Tokyo） 

```xml
<?xml version="1.0"?>
<current>
  <city id="1850147" name="Tokyo">
    <coord lat="35.69" lon="139.69"/>
    <country>JP</country>
    <sun set="2016-08-15T09:30:23" rise="2016-08-14T20:00:21"/>
  </city>
  <temperature unit="kelvin" max="304.82" min="298.71" value="301.68"/>
  <humidity unit="%" value="85"/>
  <pressure unit="hPa" value="1001"/>
  <wind>
    <speed name="Gentle Breeze" value="3.41"/>
    <gusts/>
    <direction name="South" value="179.504" code="S"/>
  </wind>
  <clouds name="clear sky" value="8"/>
  <visibility/>
  <precipitation unit="3h" value="0.245" mode="rain"/>
  <weather value="light rain" icon="10d" number="500"/>
  <lastupdate value="2016-08-15T07:41:15"/>
</current>
```

## JavaでOpenWeatherMapのAPIを呼び出す

RESTクライアントは色々ありますが、お手軽なApache Commonsのhttpclientとfluent-hcにします。

bazelに依存関係を定義します。 

WORKSPACE 

```
maven_jar (
    name = "org_apache_httpcomponents_httpcore",
    artifact = "org.apache.httpcomponents:httpcore:4.4.5"
)
maven_jar (
    name = "org_apache_httpcomponents_httpclient",
    artifact = "org.apache.httpcomponents:httpclient:4.5.2"
)
maven_jar (
    name = "org_apache_httpcomponents_fluent_hc",
    artifact = "org.apache.httpcomponents:fluent-hc:4.5.2"
)
maven_jar (
    name = "commons_logging",
    artifact = "commons-logging:commons-logging:1.2"
)
```

BUILD 

```
java_binary (
    name = "openweathermap",
    srcs = glob(["**/*.java"]),
    main_class = "gq.weizlogy.weather.wallpaper.Main",
    deps = [
        "httpcomponents"
    ]
)
java_library (
    name = "httpcomponents",
    exports = [
        "@org_apache_httpcomponents_httpcore//jar",
        "@org_apache_httpcomponents_httpclient//jar",
        "@org_apache_httpcomponents_fluent_hc//jar",
        "@commons_logging//jar"
    ]
)
```

Main.java 

```java
package gq.weizlogy.weather.wallpaper;

import org.apache.http.client.fluent.Request;
import org.apache.http.client.ClientProtocolException;
import java.io.IOException;

public class Main {
  public static void main(String[] args) {
    try {
      String r = Request.Get("http://api.openweathermap.org/data/2.5/weather?q=Tokyo&mode=xml&APPID=...").execute().returnContent().asString();
      System.out.println(r);
    } catch (ClientProtocolException e) {
      e.printStackTrace();
    } catch (IOException e) {
      e.printStackTrace();
    }
  }
}
```

実行結果は先ほどのXMLと同じです。 

## JavaでOpenWeatherMapのAPI実行結果をPOJOに変換する

文字列では扱いにくいのでPOJOを用意してJAXBでunmarshalします。 

WORKSPACE 

```
maven_jar (
    name = "org_apache_commons_commons_lang",
    artifact = "org.apache.commons:commons-lang3:3.4"
)
```

BUILD 

```
java_binary (
    name = "flickr",
    srcs = glob(["**/*.java"]),
    main_class = "gq.weizlogy.weather.wallpaper.Main",
    deps = [
        "httpcomponents",
        "commons_lang"
    ]
)
java_library (
    name = "httpcomponents",
    exports = [
        "@org_apache_httpcomponents_httpcore//jar",
        "@org_apache_httpcomponents_httpclient//jar",
        "@org_apache_httpcomponents_fluent_hc//jar",
        "@commons_logging//jar"
    ]
)
java_library (
    name = "commons_lang",
    exports = [
        "@org_apache_commons_commons_lang//jar"
    ]
)
```

CurrentWeather.java 

```java
package gq.weizlogy.weather.wallpaper;

import javax.xml.bind.annotation.XmlAttribute;
import javax.xml.bind.annotation.XmlElement;
import javax.xml.bind.annotation.XmlRootElement;
import org.apache.commons.lang3.builder.ToStringBuilder;

@XmlRootElement(name = "current")
public class CurrentWeather {
  @XmlElement
  private City city;
  @XmlElement
  private Temperature temperature;
  @XmlElement
  private Humidity humidity;
  @XmlElement
  private Pressure pressure;
  @XmlElement
  private Wind wind;
  @XmlElement
  private Clouds clouds;
  @XmlElement
  private String visibility;
  @XmlElement
  private Precipitation precipitation;
  @XmlElement
  private Weather weather;
  @XmlElement
  private Lastupdate lastupdate;

  @Override
  public String toString() {
    return ToStringBuilder.reflectionToString(this);
  }

  public static class City {
    @XmlAttribute
    private String id;
    @XmlAttribute
    private String name;
    @XmlElement
    private Coord coord;
    @XmlElement
    private String country;
    @XmlElement
    private Sun sun;

    @Override
    public String toString() {
      return ToStringBuilder.reflectionToString(this);
    }

    public static class Coord {
      @XmlAttribute
      private String lon;
      @XmlAttribute
      private String lat;
      @Override
      public String toString() {
        return ToStringBuilder.reflectionToString(this);
      }
    }
    public static class Sun {
      @XmlAttribute
      private String set;
      @XmlAttribute
      private String rise;
      @Override
      public String toString() {
        return ToStringBuilder.reflectionToString(this);
      }
    }
  }

  public static class Temperature {
    @XmlAttribute
    private String value;
    @XmlAttribute
    private String min;
    @XmlAttribute
    private String max;
    @XmlAttribute
    private String unit;
    @Override
    public String toString() {
      return ToStringBuilder.reflectionToString(this);
    }
  }

  public static class Humidity {
    @XmlAttribute
    private String value;
    @XmlAttribute
    private String unit;
    @Override
    public String toString() {
      return ToStringBuilder.reflectionToString(this);
    }
  }

  public static class Pressure {
    @XmlAttribute
    private String value;
    @XmlAttribute
    private String unit;
    @Override
    public String toString() {
      return ToStringBuilder.reflectionToString(this);
    }
  }

  public static class Wind {
    @XmlElement
    private Speed speed;
    @XmlElement
    private String gusts;
    @XmlElement
    private Direction direction;

    @Override
    public String toString() {
      return ToStringBuilder.reflectionToString(this);
    }

    public static class Speed {
      @XmlAttribute
      private String value;
      @XmlAttribute
      private String name;
      @Override
      public String toString() {
        return ToStringBuilder.reflectionToString(this);
      }
    }
    public static class Direction {
      @XmlAttribute
      private String value;
      @XmlAttribute
      private String name;
      @XmlAttribute
      private String code;
      @Override
      public String toString() {
        return ToStringBuilder.reflectionToString(this);
      }
    }
  }

  public static class Clouds {
    @XmlAttribute
    private String value;
    @XmlAttribute
    private String name;
    @Override
    public String toString() {
      return ToStringBuilder.reflectionToString(this);
    }
  }

  public static class Precipitation {
    @XmlAttribute
    private String mode;
    @Override
    public String toString() {
      return ToStringBuilder.reflectionToString(this);
    }
  }

  public static class Weather {
    @XmlAttribute
    private String value;
    @XmlAttribute
    private String number;
    @XmlAttribute
    private String icon;
    @Override
    public String toString() {
      return ToStringBuilder.reflectionToString(this);
    }
  }

  public static class Lastupdate {
    @XmlAttribute
    private String value;
    @Override
    public String toString() {
      return ToStringBuilder.reflectionToString(this);
    }
  }
}
```

Main.java 

```java
package gq.weizlogy.weather.wallpaper;

import org.apache.http.client.fluent.Request;
import org.apache.http.client.ClientProtocolException;
import java.io.IOException;
import javax.xml.bind.JAXB;
import java.io.StringReader;

public class Main {
  public static void main(String[] args) {
    try {
      String r = Request.Get("http://api.openweathermap.org/data/2.5/weather?q=Tokyo&mode=xml&APPID=...").execute().returnContent().asString();
      CurrentWeather w = JAXB.unmarshal(new StringReader(r), CurrentWeather.class);
      System.out.println(w);
    } catch (ClientProtocolException e) {
      e.printStackTrace();
    } catch (IOException e) {
      e.printStackTrace();
    }
  }
}
```

実行結果

```
gq.weizlogy.weather.wallpaper.CurrentWeather@51f102bd[
  city=gq.weizlogy.weather.wallpaper.CurrentWeather$City@25eaf052[
    id=1860785,name=Kainan,coord=gq.weizlogy.weather.wallpaper.CurrentWeather$City$Coord@6347aaf0[
      lon=135.2,lat=34.15],
    country=JP,sun=gq.weizlogy.weather.wallpaper.CurrentWeather$City$Sun@7627a57b[
      set=2016-08-21T09:39:11,rise=2016-08-20T20:24:53]],
  temperature=gq.weizlogy.weather.wallpaper.CurrentWeather$Temperature@24e16ad7[
    value=305.91,min=304.15,max=308.15,unit=kelvin],
  humidity=gq.weizlogy.weather.wallpaper.CurrentWeather$Humidity@4b2d5c2b[
    value=49,unit=%],
  pressure=gq.weizlogy.weather.wallpaper.CurrentWeather$Pressure@efe319c[
    value=1004,unit=hPa],wind=gq.weizlogy.weather.wallpaper.CurrentWeather$Wind@526b0074[
      speed=gq.weizlogy.weather.wallpaper.CurrentWeather$Wind$Speed@6eeae9f1[
        value=6.2,name=Moderate breeze],
      gusts=,direction=gq.weizlogy.weather.wallpaper.CurrentWeather$Wind$Direction@a5061b[
        value=70,name=East-northeast,code=ENE]],
  clouds=gq.weizlogy.weather.wallpaper.CurrentWeather$Clouds@5233d6f1[
    value=20,name=few clouds],
  visibility=,
  precipitation=gq.weizlogy.weather.wallpaper.CurrentWeather$Precipitation@49649260[
    mode=no],
  weather=gq.weizlogy.weather.wallpaper.CurrentWeather$Weather@69c60244[
    value=few clouds,number=801,icon=02d],
  lastupdate=gq.weizlogy.weather.wallpaper.CurrentWeather$Lastupdate@46bef49c[
    value=2016-08-21T02:13:01]]
```
