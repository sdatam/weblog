---
title: Apktool Kurulumu ve Kullanımı
date: 2018-12-20
tags: ["android", "apktool", "tools", "reverse engineering","terminal"]
---

Apktool reverse engineering için kullanılır 3rd party Android uygulamaların apk dosyalarını decompile ederek smali kodlarına dönüştürür. AndroidManifest.xml dosyasını görebilirsiniz. Uygulamaları analiz etmek için kullanabilir. İsterseniz recompile edebilirsiniz.


<!--more-->

Apktool java 8 ve üstü ile kullanılmaktadaır.
Bu blog yazılırken aşağıdaki versionlar kullanılmıştır.

os version  : Ubuntu 18.04.1 LTS
java version: openjdk version "10.0.2" 

[Apktool Web Sayfası](https://ibotpeaches.github.io/Apktool/)

### Kurulumu

1.[wrapper script](https://raw.githubusercontent.com/iBotPeaches/Apktool/master/scripts/linux/apktool) bağlantısına sağ tıklayıp "bağlantıyı farklı kaydet" seçeneğini kullanarak apktool isminde kaydediyoruz
Eğer terminal üzerinden indirmek istiyorsanız:

```console
$ wget https://raw.githubusercontent.com/iBotPeaches/Apktool/master/scripts/linux/apktool

```

2.En yeni versiyonu indirin. [all versions](https://bitbucket.org/iBotPeaches/apktool/downloads/) 

Linkten indirmek istediğiniz versiyonun linkini kopyalayarak aynı şekilde wget ile indirilebilirsiniz.

3.İndirdiğiniz dosyanın ismini apktool.jar olarak değiştirin.

4.Her iki dosyanın da çalıştırabilir olduğunu kontrol edin. Değilse;

```console

$ chmod +x apktool apktool.jar

```

5.Her iki dosyayı /usr/local/bin/ altına taşıyın

```console

$ mv apktool apktool.jar /usr/local/bin/

```

6.apktool komutu ile çalıştırabilirsiniz.



### Kullanımı

Uygulamayı decompile etmek için;

```console
$ apktool d your_app.apk
```

```console
$ apktool b your_directory
```

Eğer apk ismini kendiniz vermek istiyorsanız `-o your_apk_name.apk` parametresini kullanabilirsiniz.

Daha kapsamlı kullanım için [Apktool Documentation](https://ibotpeaches.github.io/Apktool/documentation/) inceleyebilirsiniz.

