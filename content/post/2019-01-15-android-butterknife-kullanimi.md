---
title: Android Butter Knife Kütüphanesi Kullanımı
date: 2019-01-15
tags: ["android", "butterknife", "viewinjection", "cleancode"]
---

Merhaba arkadaşlar, bugün sizlere projemde kullandığım **Butter Knife** kütüphanesinden bahsedeceğim. 
Proje büyüdükçe kod karmaşıklığı da artıyor ve kodun okunabilirliği azalıyor. Daha az satır ve okunabilir bir kod yazmak için ButterKnife kütüphanesini kullanabilirsiniz. 
<!--more-->

Butter Knife bir View Injector kütüphanesidir. Uygulamamızda bulunan bileşenlere annotationlar kullanarak direkt olarak erişebilmemizi sağlıyor. Öncelikle Butter Knife kütüphanesini projemizde kullanabilmemiz için build.gradle içerisine dahil etmemiz gerekiyor. 

```java
dependencies {
    implementation 'com.jakewharton:butterknife:10.0.0'
    annotationProcessor 'com.jakewharton:butterknife-compiler:10.0.0'
}
```
Projemize MainActivity adında bir Empty Activity ekleyelim. Layout içerisine TextView ve Button ekleyelim. Butona tıklandığında TextView içerisine Hello World yazan basit bir kod parçacığı ekleyelim. Öncelikle Butter Knife kullanmadan işlemlerimizi nasıl gerçekleştirdiğimize bakalım.  

Layout içerisindeki bileşenlere Activity üzerinden erişebilmek için **findViewById** kullanıyoruz. Butona Click Event'ını vermek için ise satır sayımızın ve kod karmaşıklığının arttığını görebilirsiniz.

**MainActivity.java**

```java
public class MainActivity extends AppCompatActivity {
    private TextView twTest;
    private Button btnTest;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
        twTest = (TextView)findViewById(R.id.twTest);
        btnTest = (Button)findViewById(R.id.btnTest);
        btnTest.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                twTest.setText("Hello World!");
            }
        });
    }
}
```

**activity_main.xml**

```xml
<?xml version="1.0" encoding="utf-8"?>
<android.support.constraint.ConstraintLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    tools:context=".MainActivity">

    <TextView
        android:id="@+id/twTest"
        android:layout_width="0dp"
        android:layout_height="0dp"
        android:layout_marginStart="45dp"
        android:layout_marginTop="200dp"
        android:layout_marginEnd="45dp"
        android:layout_marginBottom="64dp"
        android:text="TextView"
        app:layout_constraintBottom_toTopOf="@+id/btnTest"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent" />

    <Button
        android:id="@+id/btnTest"
        android:layout_width="283dp"
        android:layout_height="wrap_content"
        android:layout_marginStart="8dp"
        android:layout_marginEnd="8dp"
        android:layout_marginBottom="165dp"
        android:text="Button"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toBottomOf="@+id/twTest" />
</android.support.constraint.ConstraintLayout>
```

Aynı örneği Activity içerisinde Butter Knife kullanarak yapalım. onCreate içerisine **ButterKnife.bind(this);** satırını eklediğimizde bu sınıf içerisindeki tanımlamaları onCreate içerisinde tanımlamış gibi olmasını sağlıyor.

Bileşenlerimizi Activity'de tanımlamak için kullandığımız **findViewById** yerine **@BindView** annotation'nını kullanıyoruz. Click Eventi için yazdığımız satırlarca kod yerine **@OnClick** annotation'nını kullanarak kodumuzu daha yalın hale getirmiş oluruz.

**MainActivity.java**

```java
public class MainActivity extends AppCompatActivity {
    @BindView(R.id.twTest) TextView twTest;
    @BindView(R.id.btnTest) TextView btnTest;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
        ButterKnife.bind(this);
    }

    @OnClick(R.id.btnTest) void clickButton(){
        twTest.setText("Hello World!");
    }
}
```

[Diğer annotation'lar ve daha fazla bilgi için ziyaret ediniz.](http://jakewharton.github.io/butterknife/)
