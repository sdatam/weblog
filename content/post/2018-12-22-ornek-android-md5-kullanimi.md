---
title: Android MD5 Kullanım Örneği
date: 2018-12-22
tags: ["md5", "android"]
---

MD5 değerini TextView üzerine yazdırarak bir örnek yapalım.

Öncelikle layout dosyamıza bir TextView ekleyip id değerini textView yapalım.

textView nesnesini tanımlayalım.

<!--more-->

Android Studio version:3.2.1
targetSdkVersion:28

```java
TextView textView;
```

onCreate() metodu içerisinde işaret edelim.

```javai
textView = (TextView)findViewById(R.id.texView);
```

```java
public static final String md5(final String s) {
    final String MD5 = "MD5";
    try {
        // Create MD5 Hash
        MessageDigest digest = java.security.MessageDigest
                .getInstance(MD5);
        digest.update(s.getBytes());
        byte messageDigest[] = digest.digest();

        // Create Hex String
        StringBuilder hexString = new StringBuilder();
        for (byte aMessageDigest : messageDigest) {
            String h = Integer.toHexString(0xFF & aMessageDigest);
            while (h.length() < 2)
                h = "0" + h;
            hexString.append(h);
        }
        return hexString.toString();

    } catch (NoSuchAlgorithmException e) {
        e.printStackTrace();
    }
    return "";
}

```

md5 fonksiyonumuzu kullanarak "Test" stringini hashleyelim ve textView üzerine yazalım.

```java
textView.setText(md5("Test"));
```

```code
0cbc6611f5540bd0809a388dc95a615b
```
şeklinde bir değer olacaktır.

[Kaynak](https://stackoverflow.com/a/4846511)


