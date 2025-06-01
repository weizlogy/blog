---
layout: post
title:  "ubuntu16.04でMonoDevelopを使った開発環境"
date:   2016-06-12 10:56:00.000 09:00
categories: system-dev
---

<!--more-->

LinuxでC#を使うための環境(mono)とIDE(MonoDevelop)をインストールします。 

まずはmonoをインストールします。 

```bash
$ sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 3FA7E0328081BFF6A14DA29AA6A19B38D3D831EF
$ echo "deb http://download.mono-project.com/repo/debian wheezy main" | sudo tee /etc/apt/sources.list.d/mono-xamarin.list
$ sudo apt-get update
$ sudo apt-get install mono-complete
```

続いてMonoDevelopをインストールします。 

```bash
$ sudo apt-get install monodevelop
```

monodevelopコマンドでIDEを起動します。
