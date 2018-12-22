---
title: Android Debug Bridge(adb) Komutları
date: 2018-12-20
tags: ["adb", "android", "console", "terminal", "tools"]
---

Android Debug Bridge(adb) Android geliştiricilerinin kullandığı bir komut kütüphanesidir. ADB, emulator ya da bilgisayarınıza bağlı fiziksel cihazınızla iletişim kurulmasını sağlar.

<!--more-->

### Temel Komutları

Cihazları listelemek için;

```console

$ adb devices

```

adb kullanırken tek cihaz varsa shell erişimi için; 

```console

$ adb shell

```

Terminal üzerinde adb kullanırken eğer birden fazla cihaz ile çalışıyorsanız. adb shell komutu verebilmek için;

Emulator için;

```console

$ adb -e shell

```

Fiziksel cihaz için;

```console

$ adb -d shell

```

Aynı türde birden fazla cihaz varsa ip ya da device name ile;


```console

$ adb -s x.x.x.x:PPP shell

```

adb ile cihaza dosya göndermek ve almak için push ve pull komutları kullanılır.

```console

$ adb push test.img /sdcard/

```

Cihaz içerisinde ekran görüntüsü almak için;

```console

$ adb shell screencap -p /sdcard/screenshot.png
$ adb pull /sdcard/screenshot.png

```

Kurulu paketleri listelemek için cihaz içerisinde;

```console

$ pm list packages

```

Farklı bir kullanım: paket ismi biliniyorsa düzenli ifade ile;

```console

$ adb shell pm list packages | grep com.example.app

```





