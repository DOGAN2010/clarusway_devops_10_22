# Uygulamalı S3-01 : Temel İşlemler, S3 Web Sitesi Barındırma ve Sürüm Oluşturma

Bu uygulamalı eğitimin amacı, öğrencilere bir S3 paketinin nasıl oluşturulacağını, S3'ün statik web sitesini barındıracak şekilde nasıl yapılandırılacağını ve sürüm oluşturma ve günlüğe kaydetme konusunda anlayış kazandırmaktır.

## Öğrenme Çıktıları

Bu uygulamalı eğitimin sonunda öğrenciler;

- bir S3 kovası oluşturun,

- dosyaları S3 kovasına yükleyin ve özelleştirin,

- S3'te statik Web Sitesi dağıtın,

- S3 kova politikalarını ayarlayın,

- S3 kovasını sürüm oluşturma seçenekleriyle yapılandırın,

- günlük kayıtlarını izlemek,


## Anahat

- Bölüm 1 - S3 Kova Temel İşlemleri

- 2. Bölüm - Statik Web Sitesi için yeni bir Paket oluşturma

- Bölüm 3 - Sürüm Oluşturma ile S3 Bucket Oluşturma


## Bölüm 1 - S3 Kova Temel İşlemleri

- AWS Management Konsolundan S3 Hizmetini açın.

- Aşağıdaki özelliklere sahip 2 paket oluşturun,

```metin
Kova adı : myfirstbucket-osvaldo-01("osvaldo" yerine, öğrenciler kendi
                              clarusway öğrenci numarası)
Bölge : K.Virginia
Tüm herkese açık erişimi engelle : İşaretli (ENGELLE TUT)
Sürüm oluşturma  : Devre dışı
Etiketleme : 0 Etiketler
Varsayılan şifreleme : Yok
Nesne düzeyinde günlük kaydı : Devre dışı

```

- Açıklamak;

  - Adlandırma kuralı (benzersiz, küresel),

  - Neden bölge seçtiğimiz,

  - Fazlalık,

  - Kullanılabilirlik.

- "index.html" ve "cat.jpg" dosyalarını varsayılan değerlerle pakete yükleyin.

- Dosya ayrıntılarını gösterin.

- Tarayıcıda dosya URL'sini açın ve erişilebilir olmadığını gösterin.

- Nesneyi herkese açık hale getirmeye çalışın, "Hata Erişim reddedildi" ile karşı karşıya kalın.

- Paket izinlerini açın, herkese açık olarak değiştirin.

```
İZİNLER >> KAMU ERİŞİMİ ENGELLE>>>> DÜZENLE>>> İŞARETSİZ
```
- Yüklenen dosyayı seçin ve "Ayrıca Herkese Açık" yapın.

- Tarayıcıda dosya URL'sini açın, artık erişilebilir olduğunu gösterin.

- 'Görüntüler' olarak adlandırılan bir klasör oluşturun, bir klasörün neden S3'te önek olarak da adlandırıldığını açıklayın

- "cat1.jpg" dosyasını "resimler" klasörü altına "sürükle ve bırak" ile yükleyin.

- Tarayıcıda dosya URL'sini açın ve "Erişilemez" olduğunu gösterin.

- Yüklenen dosyayı seçin ve "Ayrıca Herkese Açık" yapın.

- Tarayıcıda dosya URL'sini açın, artık erişilebilir olduğunu gösterin.

- "myfirstbucket-osvaldo-01" paketinin altına "cat2.jpg" ve "cat3.jpg" dosyalarını yükleyin.

- "Resimler" klasörü altındaki verileri aktarmak için "taşı" işlevinin nasıl kullanılacağını gösterin.

```metin
hareket ---> cat1.jpg
```

- "cat2.jpg" dosyasının nasıl silineceğini gösterin.

```metin
sil ---> cat2.jpg
```

- "cat3.jpg" dosyasının nasıl yeniden adlandırılacağını gösterin.

```metin
cat3.jpg'yi cat_renamed.jpg olarak yeniden adlandırın
```

- "Resimler" klasörünün nasıl silineceğini gösterin,

```metin
---> resimleri sil
```

- Klasörde nesneler olsa bile silindiğini gösterin.

- S3 Kovasına bir dosya yükleyin (sürükle ve bırak olmadan) ve "İzinleri ayarla" bölümüne gidin ve depolama sınıflarını açıklayın (S3 Standart, Standart IA, Glacier: 3 AZ, Dayanıklılık 11/9)

## 2. Bölüm - Statik Web Sitesi için yeni bir Paket oluşturma

- Statik web sitesi için "pet.clarusway.static.web.hosting" adına ve aşağıdaki özelliklere sahip yeni bir paket oluşturun

```metin
Paket adı: pet.clarusway.static.web.hosting
Bölge : K.Virginia
Tüm herkese açık erişimi engelle: İşaretli (ENGELLE TUT)
Sürüm oluşturma  : ETKİN****
Etiketleme : 0 Etiketler
Varsayılan şifreleme: Yok
Nesne düzeyinde günlük kaydı : Devre dışı
```

- `pet.clarusway.static.web.hosting` S3 kovasına tıklayın ve aşağıdaki dosyaları yükleyin.

```metin
index.html
kedi.jpg
```

- "pet.clarusway.static.web.hosting" paketinin özelliklerinden statik web sitesi barındırma ayarlarını gösterin.

```
ÖZELLİKLER>>>>> STATİK WEB SİTESİ HOSTING
```

- Statik web barındırma'yı tıklayın ve "Bir web sitesini barındırmak için bu paketi kullan" seçeneğini işaretleyin ve varsayılan dosya olarak "index.html" girin.

- Uç noktayı kopyalayın ve web sitesinin Erişilemez olduğunu gösterin.

- Paket Genel Erişim durumunu KONTROL EDİLDİ(ENGELLENMİŞ) yerine KONTROL EDİLMEDİ(KAMU) olarak değiştirin.

```
İZİNLER >> KAMU ERİŞİMİ ENGELLE>>>> DÜZENLE>>> İŞARETSİZ
```
- Statik web sitesi paket politikasını aşağıda gösterildiği gibi (İZİNLER >> KEPÇE POLİTİKASI) ayarlayın ve "bucket-name"yi kendi paketinizle değiştirin.

!!!! Aşağıda görülen komut dosyasından değil 'aws-s3-static-website-policy.json' dosyasını kullanın. Girinti hatası alabilirsiniz.

```
{
"Sürüm": "2012-10-17",
"Beyan": [
{
"Sid": "PublicReadGetObject",
"Efekt": "İzin ver",
"Müdür": "*",
"Eylem": "s3:GetObject",
"Resource": "arn:aws:s3:::beni değiştirmeyi unutma/*"
}
]
}
```

- Statik web sitesi URL'sini tarayıcıda açın ve çalıştığını gösterin.

- "pet.clarusway.static.web.hosting" adlı paketin altında "kitten" adlı klasör oluşturun.

- `index.html` ve `cat.jpg` dosyalarını "yavru kedi" klasörüne taşıyın.

- Statik web sitesi URL'sini tarayıcıda tekrar açın, varsayılan URL ile çalışmadığını ve "404 Bulunamadı" ile karşı karşıya olduğunu gösterin

- Dosya adı olmadan içeriği göstermek için URL'nin sonuna "kitten" yolunu ekleyin.

```metin
http://.......a
- "Kitten" klasörünün altındaki "index.html"yi "cute.html" olarak yeniden adlandırın.

- Statik web sitesi URL'sini tarayıcıda "yavru kedi" eklenmiş tekrar açın, varsayılan index.html"yle olduğu gibi çalışmadığını gösterin "404 Bulunamadı" ile karşı karşıya

- Özellikler >> statik web barındırma bölümüne gidin ve index.html'yi şirin.html olarak değiştirin.

```metin
index.html ---> en şirin.html
```

- İçeriği göstermek için uç noktayı kopyalayın ve web tarayıcısını URL'nin sonunda "kedi yavrusu" yolu ile yapıştırın.

```metin
http://.......amazonaws.com/kitten/
```

## Bölüm 3 - Sürüm Oluşturma ile S3 Kovası Oluşturma

- Aşağıdaki özelliklere sahip "pet.clarusway.versioning" adlı yeni bir paket oluşturun.

```metin
Kova adı: pet.clarusway.versioning
Bölge : K.Virginia
Tüm herkese açık erişimi engelle: KONTROL EDİLMEDİ(KAMU)*****
Sürüm oluşturma  : ETKİN****
Etiketleme : 0 Etiketler
Varsayılan şifreleme: Yok
Nesne düzeyinde günlük kaydı : Devre dışı

```

- S3 kovası `pet.clarusway.versioning`e tıklayın ve aşağıdaki dosyaları yükleyin.

```metin
index.html
kedi.jpg
```

- "pet.clarusway.versioning" paketinin özelliklerinden statik web sitesi barındırma ayarlarını gösterin.
```
ÖZELLİKLER>>>>> STATİK WEB SİTESİ HOSTING
```
- Statik web barındırma'yı tıklayın ve "Bir web sitesini barındırmak için bu paketi kullan" seçeneğini işaretleyin ve varsayılan dosya olarak "index.html" girin.

- Statik web sitesi paket politikasını aşağıda gösterildiği gibi (İZİNLER >> KEPÇE POLİTİKASI) ayarlayın ve "bucket-name"yi kendi paketinizle değiştirin.

``` json
{
"Sürüm": "2012-10-17",
"Beyan": [
{
"Sid": "PublicReadGetObject",
"Efekt": "İzin ver",
"Müdür": "*",
"Eylem": "s3:GetObject",
"Resource": "arn:aws:s3:::beni değiştirmeyi unutma/*"
}
]
}
```

- Statik web sitesi URL'sini tarayıcıda açın ve çalıştığını gösterin.

- Dosyaların sürümlerini 'pet.clarusway.versioning' paketinin hemen altında gösterin

- "index.html"yi silin.

- 'Liste sürümü' sekmesinden sürüm seçeneğini 'AÇIK' konumuna getirin.

- `index.html` dosyasının hala kovada olduğunu gösterin.

- "index.html" dosyasının altındaki "sil işaretini" göster.

- İndex.html'nin "silme işaretçilerini" silin ve yeniden mevcut olduklarını gösterin.

- VS Code ile yerelden `index.html` dosyasını açın ve ifadeyi aşağıda gösterildiği gibi değiştirin.

```metin
<center><h1> Benim Sevimli Kedim Köken</h1><center>
    | | |
    | | |
    | | |
    V V V
<center><h1> Sevimli Kedim Sürüm 1</h1><center>
```

- "index.html" dosyasının yeni bir sürümünü yükleyin.

- 'Liste sürümü' sekmesinden 'AÇIK' sürüm seçeneğini çevirin ve 'index.html'nin iki sürümünü görün.

- Statik web sitesi URL'sini tarayıcıda tekrar açın, yeni içeriği (Sürüm 1) gösterdiğini gözleyin.

- Yine 'index.html'yi VS Code ile yerelden açın ve aşağıda gösterildiği gibi deyimi değiştirin.

```metin
<center><h1> Sevimli Kedim Sürüm 1</h1><center>
    | | |
    | | |
    | | |
    V V V
<center><h1> Sevimli Kedim Sürüm 2</h1><center>
```

- "index.html" dosyasının en yeni sürümünü pakete yükleyin.

- 'Liste sürümü' sekmesinden 'AÇIK' sürüm seçeneğini açın ve 'index.html'nin üç sürümünü görün.

- Statik web sitesi URL'sini tarayıcıda tekrar açın, yeni içeriği gösterdiğini (Sürüm 2) gözlemleyin.

- İndex.html'nin sürümlerini gösterin ve en son sürümleri silin.

- Statik web sitesi URL'sini tarayıcıda tekrar açın, "Sürüm 1" içeriğini gösterdiğini gözleyin.