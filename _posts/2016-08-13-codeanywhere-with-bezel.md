---
layout: post
title:  "Codeanywhereでbazelを使う"
date:   2016-08-13 17:06:00.000 09:00
categories: system-dev
---

[Codeanywhere](https://codeanywhere.com/)はクラウドIDEで、sudoが許可されたターミナルを使うことができます。
Google+アカウント連携ですぐに使えます。

[bazel](http://bazel.io/)は、mavenやGradleのようなビルドツールで、様々な言語のビルドが可能です。

## Codeanyhwereにbazelをインストール

bazelはjdk1.8以降（jdk1.7はサポートされているが非推奨）が必須ですが、Codeanywhereはjdk1.7の環境です。
今回はjdk1.7のままでインストールします。 

```bash
cabox@box-codeanywhere:~/workspace$ java -version
java version "1.7.0_95"
OpenJDK Runtime Environment (IcedTea 2.6.4) (7u95-2.6.4-0ubuntu0.14.04.1)
OpenJDK 64-Bit Server VM (build 24.95-b01, mixed mode)
```

[Installig Bazel](http://bazel.io/docs/install.html)を参考に、以下のコマンドを打ちます。

```bash
$ echo "deb [arch=amd64] http://storage.googleapis.com/bazel-apt testing jdk1.7" | sudo tee /etc/apt/sources.list.d/bazel.list
$ curl https://storage.googleapis.com/bazel-apt/doc/apt-key.pub.gpg | sudo apt-key add -
sudo apt-get update && sudo apt-get install bazel
```

## bazelでjavaをビルド

最低限の必要なファイルを作成します。 

```bash
cabox@box-codeanywhere:~/workspace$ mkdir -p hello/src/main/java/gq/weizlogy
cabox@box-codeanywhere:~/workspace$ touch hello/src/main/java/gq/weizlogy/Main.java
cabox@box-codeanywhere:~/workspace$ touch hello/WORKSPACE
cabox@box-codeanywhere:~/workspace$ touch hello/BUILD
```

hello/src/main/java/gq/weizlogy/Main.java 

```java
package gq.weizlogy;
public class Main {
    public static void main(String[] args) {
        System.out.println("Hello Bazel.");
    }
}
```

hello/WORKSPACEは空ファイルで構いません。 

hello/BUILD 

```
java_binary (
    name = "hello",
    srcs = glob(["**/*.java"]),
    main_class = "gq.weizlogy.Main"
)
```

ビルドします。 

```bash
cabox@box-codeanywhere:~/workspace$ cd hello
cabox@box-codeanywhere:~/workspace/hello$ bazel build //:hello
WARNING: Sandboxed execution is not supported on your system and thus hermeticity of actions cannot be guaranteed. See http://bazel.io/docs/bazel-user-manual.html#sandboxing for more information. You can turn off this warning via --ignore_unsupported_sandboxing.
INFO: Found 1 target...
Target //:hello up-to　date:
  bazel-bin/hello.jar
  bazel-bin/hello
INFO: Elapsed time: 5.876s, Critical Path: 1.20s
```

WARNINGがでています。CodeanywhereのコンテナはSandboxed executionをサポートしていないので、ビルドオプションを付与します。 

```bash
cabox@box-codeanywhere:~/workspace/hello$ bazel build --ignore_unsupported_sandboxing //:hello
```

実行します。 

```bash
cabox@box-codeanywhere:~/workspace/hello$ ./bazel-bin/hello
Hello Bazel.
```
