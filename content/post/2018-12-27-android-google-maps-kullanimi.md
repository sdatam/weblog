---
title: Google Maps API Kullanımı
date: 2018-12-27
tags: ["android", "googlemaps", "apikey", "maps"]
---

**API Key Oluşturma**

Bildiğiniz üzere Google Maps dünyada en çok kullanılan haritalardan birisidir. Google Maps'i Android Projemizde kullanabilmek için öncellikle Google Developer Console adresinden bir key almamız gerekiyor. 

<!--more-->

![Proje Oluştur](http://resimag.com/p1/63b9e5cd5f.png)

Bunun için öncellikle bir Gmail adresiyle giriş yapmak gerekiyor. Giriş yaptıktan sonra karşımıza çıkan sayfada bulunan **PROJE OLUŞTUR** yazısına tıklayalım. 

![Proje Adı](http://resimag.com/p1/763f5e1fa9.png)

Projemiz için bir isim belirleyelim ve oluştur butonuna tıklayalım.

![Maps SDK For Android](http://resimag.com/p1/0bfce32373.png)

Karşımıza çıkan sayfada **Maps SDK For Android**'e tıklayalım ve etkinleştirelim.

![Hizmetler](http://resimag.com/p1/df01b79df4.png)

Solda bulunan menüye tıklayarak API'ler ve Hizmetler Sekmesinin altında bulunan Kontrol Paneline tıklayalım. 

![Kimlik Bilgileri](http://resimag.com/p1/774faa4caa.png)

Burada Kimlik bilgilerini oluştur tıkladığımızda karşımıza 3 seçenek çıkıyor. Buradan API Anahtarını seçelim. Bu şekilde API Anahtarını almış olduk. Projemizden sadece bizim bu API'ye erişebilmemiz için kısıtlama yapmamız gerekecektir. Anahtarı kısıtla butonuna tıklayalım.

![Kimlik Bilgileri](http://resimag.com/p1/5dfbcc9ae0.png)

Artık uygulamamızı kısıtlayabileceğiz. Uygulama kısıtlamaları bölümünden **Android Uygulamaları** seçeneğini işaretleyelim. Uygulamamızın Paket Adı ve Fingerprint bilgilerimizle beraber satır bazında ekleme yapmamız gerekecek.

![SHA-1](http://resimag.com/p1/00cbc7074d.png)

SHA-1 Sertifikasını bulabilmek için Android Studiodaki Projemizi açarak sağ bölümde bulunan **GRADLE** penceresini açalım. **Proje Adı -> Tasks ->
signingReport** seçtikten sonra signingReport'un üzerine tıkladığımızda bize SHA-1 değerini verir. Console'dan bu SHA-1 değerini kopyalayıp yapıştırabilirsiniz.

![Maps Activity](http://resimag.com/p1/4d0bd384d4.png)

Daha önceden oluşturduğunuz bir Android Studio Projesi varsa Paket Adına sağ tıklayıp **New -> Activity -> Gallery -> Google Maps Activity**'i seçerek yeni bir Activity oluşturabilirsiniz. 

![Google Maps API xml](http://resimag.com/p1/9171a50081.png)

Yeni Activity oluştuktan sonra **res -> values -> google_maps_api.xml** klasörünün içerisinde YOUR_KEY_HERE yazan 
yere API Anahtarını yapıştırabilirsiniz. 

![Google Maps API xml](http://resimag.com/p1/62ec2a7d6e.png)

Daha sonra API anahtarını Manifest dosyasının içerisine de yapıştıralım.

### Kodlamaya Başlayalım

MapsActivity'i otomatik olarak oluşturulduğunda içerisinde bazı hazır kodlar bulunuyor. Tam olarak bu kodların ne yaptığından bahsedelim.

Projemizde haritaları kullanmanın en kolay yolu **SupportMapFragment** kullanmaktır. Bunun için **activity_maps.xml** dosyamızın içerisine bir fragment bileşeni eklememiz gerekiyor.

```xml
<?xml version="1.0" encoding="utf-8"?>
<fragment xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:map="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:id="@+id/map"
    android:name="com.google.android.gms.maps.SupportMapFragment"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    tools:context=".MapsActivity" />
```

**getMapAsync()** otomatik olarak haritalar sistemini ve görünümü başlatır. **onMapReady()** harita kullanıma hazır olduğunda tetiklenir. Harita üzerinde belirli bir noktayı işaretlemek için Marker oluşturmamız gerekir. Bunun için öncelikle enlem ve boylam
bilgilerini belirtmemiz gerekiyor. LatLng sınıfını kullanarak enlem ve boylam bilgilerini parametre olarak eklememiz gerekir.
Daha sonra bu enlem ve boylam üzerine Marker eklemek için **addMarker()** methodu kullanılır.

```java
package testapp.sdatam.sdatam;

import android.support.v4.app.FragmentActivity;
import android.os.Bundle;
import com.google.android.gms.maps.CameraUpdateFactory;
import com.google.android.gms.maps.GoogleMap;
import com.google.android.gms.maps.OnMapReadyCallback;
import com.google.android.gms.maps.SupportMapFragment;
import com.google.android.gms.maps.model.LatLng;
import com.google.android.gms.maps.model.MarkerOptions;

public class MapsActivity extends FragmentActivity implements OnMapReadyCallback {


    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_maps);
        // Obtain the SupportMapFragment and get notified when the map is ready to be used.
        SupportMapFragment mapFragment = (SupportMapFragment) getSupportFragmentManager()
                .findFragmentById(R.id.map);
        mapFragment.getMapAsync(this);
    }

    @Override
    public void onMapReady(GoogleMap googleMap) {
        // Add a marker in Sydney, Australia,
        // and move the map's camera to the same location.
        LatLng sydney = new LatLng(-33.852, 151.211);
        googleMap.addMarker(new MarkerOptions().position(sydney)
                .title("Marker in Sydney"));
        googleMap.moveCamera(CameraUpdateFactory.newLatLng(sydney));
    }
}
```
![Maps Activity](http://resimag.com/p1/9fa85a69a0.png)

 
