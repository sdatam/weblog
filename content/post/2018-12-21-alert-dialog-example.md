---
title: Alert Dialog Örneği
date: 2018-12-21
tags: ["alertdialog", "android", "dialogs", "android studio"]
---

### Nedir?

Android Studio üzerinde uygulama geliştirirken şöyle bir durum ile karşılaştım. 
Layout kullanmadan bir dialog oluşturmam gerekiyordu. Bu dilog üzerindeki butonun onclick durumu tetiklendiğinde işlem yaptırmam gerekiyordu.
Bu durum için alertdialog kullandım. Eğer istediğiniz boyutlarda ve özelliklerde dialog olsun isterseniz layout ile birlikte custom dialog kullanabilirsiniz. 

<!--more-->

Android Studio version:3.2.1
targetSdkVersion:28

```java

final AlertDialog.Builder alertDialog = new AlertDialog.Builder(MainActivity.this);
alertDialog.setTitle("Başlık Giriniz");
final EditText input = new EditText(MainActivity.this);   //Mainactivity içerisinde kullandığım için

LinearLayout.LayoutParams lp = new LinearLayout.LayoutParams(
        LinearLayout.LayoutParams.MATCH_PARENT,
        LinearLayout.LayoutParams.MATCH_PARENT);
input.setLayoutParams(lp);
alertDialog.setView(input);


alertDialog.setPositiveButton("KAYDET",
        new DialogInterface.OnClickListener() {
            public void onClick(DialogInterface dialog, int which) {
               		  //TODO: tetiklenince yaptırmak istediğiniz
            }
        });
alertDialog.show();
```

Daha fazlası için: Android dokümantsyonunda [Dialogs](https://developer.android.com/guide/topics/ui/dialogs) sayfasını inceleyebilirsiniz.
