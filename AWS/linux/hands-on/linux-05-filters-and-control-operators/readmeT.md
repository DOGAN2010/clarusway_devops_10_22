# Uygulamalı Linux-05 : Filtreler ve Kontrol Operatörleri
​
Bu uygulamalı eğitimin amacı, öğrencilere Linux'ta filtrelerin ve kontrol operatörlerinin nasıl kullanılacağını öğretmektir.
​
## Öğrenme Çıktıları
​
Bu uygulamalı eğitimin sonunda öğrenciler;
​
- Filtre komutlarını kullanın.
​
- Boru komutları.
​
- Kontrol operatörlerini kullanın.
​
## Anahat
​
- Bölüm 1 - Filtreleri Kullanma
​
- Bölüm 2 - Kontrol Operatörlerini Kullanma
​
## Bölüm 1 - Filtreleri Kullanma
​
**kedi**

- dosyaları birleştirin ve standart çıktıya yazdırın
​
- Bir klasör oluşturun ve filtreler olarak adlandırın.
​
```bash
mkdir filtreleri
cd filtreleri
```
- "days.txt" adında bir "metin" dosyası oluşturun.
​
```bash
vim gün.txt
```
​
```bash
Pazartesi
Salı
Çarşamba
Perşembe
Cuma
Cumartesi
Pazar
```
- days.txt içeriğini görüntüleyin.
```bash
kedi günleri.txt
```
- Bir boruda kullanıldığında cat komutunun ne yaptığını gösterin.
​
```bash
kedi günleri.txt | kedi | kedi | kedi | kedi
```
- 'count.txt' adında bir 'metin' dosyası oluşturun.
​
```bash
nano sayım.txt
```
```metin
bir
2
üç
dört
beş
altı
Yedi
sekiz
dokuz
on
on bir
```
- count.txt içeriğini görüntüleyin.

```bash
kedi sayısı.txt
```

**tiş**

- Standart girdiden okuma ve standart çıktı ve dosyalara yazma
​
- count.txt dosyasının içeriğini temp.txt adlı başka bir dosyaya ters sırada yazın ve temp.txt içeriğini ters sırada görüntüleyin.

```bash
tac sayısı.txt | tee temp.txt | tak
```
- Temp.txt dosyasının oluşturulup oluşturulmadığını kontrol edin ve içeriği görüntüleyin.
​
```bash
ls
kedi temp.txt
```

**grep**
​
- Desenlerle eşleşen satırları yazdırın. Grep'in en yaygın kullanımı, belirli bir dizeyi içeren (veya içermeyen) metin satırlarını filtrelemektir.

- "tennis.txt" adında bir "metin" dosyası oluşturun.
​
```bash
kedi > tenis.txt
​
Amelie Mauresmo, Fra
Justine Henin, BEL
Serena Williams, ABD
Venüs Williams, ABD
```
>>EOF için ctrl+d tuşlarına basın**
​
- Tennis.txt içeriğini görüntüleyin.

```bash
kedi tenisi.txt
```

- Yalnızca 'Williams' içeren tenis.txt satırlarını görüntüleyin.
​
```bash
kedi tenis.txt | grep Williams
```

- Yalnızca 'bizi' içeren tenis.txt satırlarını görüntüleyin.
​
```bash
kedi tenis.txt | bizi grep
```

- Geçerli dizindeki tüm dosyaların sahipler sütununu (3. sütun) görüntüleyin.
​
**kesmek**

- Kesme filtresi, sınırlayıcıya veya bayt sayısına bağlı olarak dosyalardan sütunlar seçebilir
​
```bash
ls -l | kes -d' ' -f3
```

- /etc/passwd dizininin içeriğini görüntüleyin.
​
```bash
kedi /etc/passwd
```

- Yalnızca kullanıcı adlarını görüntüleyin.
​
```bash
cut -d: -f1 /etc/passwd
```

**tr**
​
- 'tr' komutu 'çevir' anlamına gelir. Küçük harften büyük harfe veya tam tersi veya yeni satırları boşluklara çevirmek için kullanılır.

- 'clarusway.txt' adında bir 'metin' dosyası oluşturun.
​
```bash
kedi << EOF > clarusway.txt
Clarusway:Kendinizi yeniden keşfetmenin yolu.
EOF
```

- clarusway.txt içeriğini görüntüleyin.
​
```bash
kedi clarusway.txt
```

- clarusway.txt içeriğinde, aer harflerini 'QAZ' ile değiştirin veya çevirin.
​
```bash
kedi clarusway.txt | tr aer QAZ
```
​
- Aynı satıra count.txt dosyasının içeriğini yazın.
​
```bash
kedi sayısı.txt | tr '\n' '
```
​
- clarusway.txt içeriğindeki tüm sesli harfleri silin.
​
```bash
kedi clarusway.txt | tr -d aeiou
```
​
- clarusway.txt dosyasının tüm içeriğini büyük harflerle yazın.
​
```bash
kedi clarusway.txt | tr [a-z] [A-Z]
```

**tuvalet**
​
- Her dosya için satır, kelime ve karakter yazdırın.

- count.txt içeriğindeki satırları, kelimeleri ve harfleri sayın.
​
```bash

wc sayısı.txt
```

- Bilgisayarda kaç kullanıcı olduğunu bulun.

```bash
wc -l /etc/passwd
```

**çeşit**
​
- Sıralama filtresi varsayılan olarak alfabetik bir sıralamaya sahip olacaktır. Sıralama filtresi varsayılan olarak alfabetik bir sıralamaya sahip olacaktır.

- "marks.txt" adında bir "metin" dosyası oluşturun.
​
```bash
kedi << EOF > mark.txt
hava-9
albert-9
james-9
john-10
zeytin-7
tom-7
galip-10
walter-8
EOF
```
- Marks.txt içeriğini görüntüleyin.
​
```bash
kedi işaretleri.txt
```

- Marks.txt dosyasının içeriğini sıralayın.
​
```bash
mark.txt dosyasını sırala
```

- Marks.txt içeriğini ters sırada sıralayın.
​
```bash
sıralama -r mark.txt
```

**tek**
​
- tekrarlanan satırları bildirin veya atlayın. uniq komutu yardımıyla, her kelimenin sadece bir kez geçeceği sıralı bir liste oluşturabilirsiniz.

- "trainees.txt" adında bir "metin" dosyası oluşturun.
​
```bash
kedi << EOF > kursiyerler.txt
John
james
hava
zeytinci
walter
albert
james
John
travis
mikrofon
hava
Thomas
Daniel
John
hava
zeytinci
mikrofon
John
EOF
```

- Trainees.txt dosyasının içeriğini görüntüleyin.
​
```bash
kedi kursiyerleri.txt
```

- Trainees.txt içeriğinde yalnızca benzersiz adları görüntüleyin.
​
******uniq komutunu kullanmadan önce dosyanın sıralanması gerekir******
​
```bash
kursiyerler.txt dosyasını sırala | tek
```

**iletişim**

- Sıralanmış iki dosyayı satır satır karşılaştırın. Varsayılan olarak, 'comm' her zaman üç sütun görüntüler.
İlk sütun, ilk dosyanın eşleşmeyen öğelerini, ikinci sütun eşleşmeyen öğeleri gösterir
ikinci dosyanın ve üçüncü sütun, her iki dosyanın eşleşen öğelerini gösterir.

- 'comm' komutunun uygulanabilmesi için her iki dosyanın da sıralı olması gerekir.
​
- 'file1.txt' adında bir 'metin' dosyası oluşturun.
​
```bash
kedi << EOF > dosya1.txt
aeron
Fatura
James
John
Oliver
Walter
EOF
```

- "file2.txt" adında başka bir "metin" dosyası oluşturun.
​
```bash
kedi << EOF > dosya2.txt
kurnazlık
James
John
Raymond
EOF
```

- file1.txt ve file2.txt dosyasını karşılaştırın.
​
******comm komutunu kullanmadan önce dosyalar sıralanmalıdır******
​
```bash
iletişim dosyası1.txt dosya2.txt
```

- EGZERSİZ YAPMAK:
​
  - `countries.csv` adlı bir dosya oluşturun.
​
```bash
kedi << EOF > country.csv
Ülke, Başkent, Kıta
ABD, Washington, Kuzey Amerika
Fransa, Paris, Avrupa
Kanada, Ottawa, Kuzey Amerika
Almanya, Berlin, Avrupa
EOF
```
  - Yalnızca 'Kıta' sütununu kes | Başlığı kaldır | Çıktıyı Sırala | Farklı değerleri listele | 'continent.txt' dosyasına kaydedin ve ekranda görüntüleyin.
​
```bash
****************************************
```
## Bölüm 2 - Kontrol Operatörlerini Kullanma
​
>**;**
​
- `;` ile tek satırda birden fazla komut kullanılabilir.

- Aynı satıra ; kullanarak iki ayrı cat komutu yazın.
​
```bash
kedi günleri.txt ; kedi sayısı.txt
```

```bash
yankı Merhaba; yankı Dünya!
```

>**&**

- Bir satır ve işareti & ile bittiğinde, kabuk komutun bitmesini beklemez. Kabuk isteminizi geri alacaksınız ve komut arka planda yürütülüyor. Bu komut arka planda çalışmayı bitirdiğinde bir mesaj alacaksınız.
​
- sleep 10 komutunu çalıştırın ve bu komutun işlemi bitene kadar çekirdeğin meşgul olduğunu gösterin.
​
```bash
uyku 10
```

- Sleep 20 komutunu çalıştırın ve diğer komutları çalıştırırken bu komutun arkasında çalışmasına izin verin.
​
```bash
uyku 20 &
ls -l
kedi sayısı.txt
kedi günleri.txt
```

>>$?**
​
- Bu kontrol operatörü, son yürütülen komutun durumunu kontrol etmek için kullanılır. Durum '0' gösteriyorsa komut başarıyla yürütülmüştür ve '1' gösteriliyorsa komut başarısız olmuştur.

- ls komutunu çalıştırın ve başarıyla yürütüldüğünü gösterin.
​
```bash
ls
yankı $?
```

- lss komutunu çalıştırın ve başarısız olduğunu gösterin.
​
```bash
ls
yankı $?
```

>**&&**

- Komut kabuğu, &&'yi mantıksal AND olarak yorumlar. Bu komutu kullanırken, ikinci komut yalnızca birincisi başarıyla yürütüldüğünde yürütülür.
​
- days.txt dosyasını görüntüleyin ve düzgün çalışıyorsa count.txt dosyasını görüntüleyin.
​
```bash
kedi günleri.txt && kedi sayısı.txt
```

- days.text'i görüntüleyin ve düzgün çalışıyorsa count.txt'yi görüntüleyin.
​
```bash
kedi günleri.metin && kedi sayısı.txt
```

>>||**

- Komut kabuğu, (||) mantıksal 'VEYA' olarak yorumlar. Bu, mantıksal "VE"nin tersidir. İkinci komutun yalnızca ilk komut başarısız olduğunda yürütüleceği anlamına gelir.
​
- Days.txt dosyasını görüntüleyin veya ekrana 'clarusway' yazın, ardından 'one' yazın.
​
```bash
kedi günleri.txt || yankı clarusway ; yankı bir
```

- Ekrana 'birinci' veya 'ikinci' yazıp ardından 'üçüncü' yazın.
​
```bash
ilk yankı || yankı saniye ; yankı üçüncü
önce zecho || yankı saniye ; yankı üçüncü
```

>>&& ve ||**

- Bu mantıksal AND ve mantıksal OR'yi komut satırında if-then-else yapısını yazmak için kullanabiliriz. Bu örnek, rm komutunun başarılı olup olmadığını görüntülemek için yankı kullanır.
​
- file1.txt dosyasının bir kopyasını oluşturun ve dosya11.txt olarak adlandırın.
​
```bash
cp dosya1.txt dosya11.txt
```
- file11.txt dosyasını silin ve düzgün silinmişse bir mesaj yazın.
​
```bash
rm file11.txt && echo 'işe yaradı' || echo 'başarısız oldu'
```
- Son komutu tekrar çalıştırın.
​
```bash
rm file11.txt && echo 'işe yaradı' || 'başarısız oldu'
```

>**#**

- Sayı işaretinden (#) sonra yazılan her şey kabuk tarafından yok sayılır. Bu, bir kabuk yorumu yazmak için kullanışlıdır ancak komut yürütme veya kabuk genişletme üzerinde hiçbir etkisi yoktur.​

- echo komutunu çalıştırın ve bir yorum satırı ekleyin.
​
```bash
echo '# yorum işaretidir' # echo komutu kendisinden sonra gelen dizeyi görüntüler.
yankı # yorum işaretidir
echo \# yorum işaretidir
```

>** \ **
- Sayı işaretinden (#) sonra yazılan her şey kabuk tarafından yok sayılır. Bu, bir kabuk yorumu yazmak için kullanışlıdır ancak komut yürütme veya kabuk genişletme üzerinde hiçbir etkisi yoktur.​

- echo komutunu çalıştırın ve bir yorum satırı ekleyin.
​
```bash
echo '# yorum işaretidir' # echo komutu kendisinden sonra gelen dizeyi görüntüler.
yankı # yorum işaretidir
echo \# yorum işaretidir
```

>** \ **

- Ters eğik çizgi ile biten satırlar bir sonraki satırda devam ettirilir. Kabuk, yeni satır karakterini yorumlamaz ve ters eğik çizgi içermeyen bir satırsonu ile karşılaşılıncaya kadar kabuk genişlemesini ve komut satırının yürütülmesini bekler.

- Kaçan karakterler, kabuk genişletmesinde kontrol karakterlerinin kullanımını sağlamak için ancak kabuk tarafından yorumlanmadan kullanılır.
​
- Birden çok satırda tek bir komut çalıştırın.
​
```bash
echo bu komut yazıldı \
sadece tek bir satırda değil \
ama aynı zamanda birden fazla satırda.
```
- Ekrana şu cümleyi yazın: Özel karakterler *, \, ", #, $, '.
​
```bash
echo Özel karakterler \*, \\, \", \#, \$, \' şeklindedir.
```

- EGZERSİZ YAPMAK:
​
  1 A. Geçerli dizinde “clarusway.doc” arayın
    B. Varsa içeriğini görüntüleyin
    C. Mevcut değilse, “Çok erken!” Yazdır mesajı.
  2. “Tebrikler” içeren “clarusway.doc” adlı bir dosya oluşturun
  3. Adım 1'i tekrarlayın
​
```bash
****************************************
```