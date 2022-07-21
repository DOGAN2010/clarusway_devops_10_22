# Uygulamalı Linux-06 : Kabuk Komut Dosyası Temelleri

Bu uygulamalı eğitimin amacı, öğrencilere kabukta nasıl komut dosyası yazılacağını öğretmektir.

## Öğrenme Çıktıları

Bu uygulamalı eğitimin sonunda öğrenciler;

- kabuk komut dosyası oluşturma temellerini açıklar.

- kabuk değişkenlerini açıklar.

- basit aritmetik yapın.

## Anahat

- Bölüm 1 - Kabuk Komut Dosyası Temelleri

- Bölüm 2 - Kabuk Değişkenleri

- Bölüm 3 - Basit Aritmetik

## Bölüm 1 - Kabuk Komut Dosyası Temelleri

- Bir klasör oluşturun ve onu kabuk komut dosyası olarak adlandırın.

```bash
mkdir kabuk komut dosyası oluşturma && cd kabuk komut dosyası oluşturma
```

- "basic.sh" adında bir "komut dosyası" dosyası oluşturun. Tüm komut dosyalarının .sh uzantısına sahip olacağını unutmayın.

```bash
#!/bin/bash
echo "Merhaba Dünya"
```

- Komut dosyamıza başka bir şey eklemeden önce, sistemi bir kabuk komut dosyasının başlatıldığı konusunda uyarmamız gerekiyor.
Bu, ilk satırda `#!/bin/bash` belirtilerek yapılır, bu da betiğin her zaman başka bir kabuk yerine bash ile çalıştırılması gerektiği anlamına gelir. '#!', 'şebang' olarak adlandırılır, çünkü '#' sembolüne karma, '!' sembolüne ise patlama denir.

- Yukarıdaki içeriği kaydettikten sonra betiği çalıştırılabilir hale getirmemiz gerekiyor.

```bash
chmod +x basic.sh
```

- O zaman `basic.sh` dosyasını çalıştırabiliriz. basic.sh'yi yürütmek için, "basic.sh" dosyasının başına "./" eklenmesi gerekir. `./` geçerli çalışma dizininde bir şey çağırdığımız anlamına gelir. $PATH değişkenimizin dışındalarsa, yürütülebilir dosyaların yolunu belirtmeliyiz.

```bash
./basic.sh
```

- Diğer kabuk komutlarını scriptimize ekleyebiliriz.

```bash
#!/bin/bash
yankı "merhaba"
tarih
pwd
ls
```

- Ve tekrar yürüt.

```bash
./basic.sh
```

### Kabuk Yorumları

- Bash, "(#)" karma işaretinden sonraki satırda yazılan her şeyi yok sayar. Bu kuralın tek istisnası, komut dosyasının "#!" karakterleriyle başlayan ilk satırıdır.

- Yorumlar satırın başına veya diğer kodlarla satır içi olarak eklenebilir. `basic.sh` dosyasını güncelleyelim.

```bash
#!/bin/bash
yankı "merhaba"
# tarih
pwd # Bu bir satır içi yorumdur
# ls
```

- Çoğu programlama dilinin aksine Bash, çok satırlı yorumları desteklemez. Ancak bunun için 'buradaki belgeyi' kullanabiliriz. Linux'ta, burada belge (yaygın olarak "heredoc" olarak da anılır), bir komuta yönlendirilecek çok satırlı dizeleri içeren özel bir kod bloğuna atıfta bulunur. HereDoc bloğu bir komuta yönlendirilmezse, çok satırlı bir yorum yer tutucusu olarak hizmet edebilir.

### HEREDOC sözdizimi

- Bir heredoc, **<<** `(yönlendirme operatörü)` ve ardından bir sınırlayıcı belirtecinden oluşur. Sınırlayıcı belirtecinden sonra, içeriği oluşturmak için dize satırları tanımlanabilir. Son olarak, sınırlayıcı belirteci, sonlandırma olarak hizmet etmek üzere sona yerleştirilir. Sınırlayıcı belirteci, içerikte görünmeyecek kadar benzersiz olduğu sürece herhangi bir değer olabilir.

- HereDoc'u nasıl kullanacağımızı görelim.

```bash
kedi << EOF
Linux Derslerine hoş geldiniz.
Bu ders kabuk komut dosyası oluşturma hakkındadır
EOF
```

- `basic.sh` dosyasını güncelleyin.

```bash
#!/bin/bash
yankı "merhaba"
# tarih
pwd # Bu bir satır içi yorumdur
# ls

kedi << EOF
Linux Derslerine hoş geldiniz.
Bu ders kabuk komut dosyası oluşturma hakkındadır
EOF

<< çok satırlı yorum
pwd
ls
içindeki her şey
HereDoc gövdesi
çok satırlı yorum
çok satırlı yorum
```

- basic.sh'yi yürütün.

```bash
./basic.sh
```

## Bölüm 2 - Kabuk Değişkenleri

- Değişken, gerçek verilere işaretçidir. Kabuk, değişkenler oluşturmamızı, atamamızı ve silmemizi sağlar.

- Bir değişkenin adı yalnızca harflerden (a'dan z'ye veya A'dan Z'ye), rakamlardan (0'dan 9) veya alt çizgi karakterinden (_) ve bir harf veya alt çizgi karakterinden oluşabilir.

- Aşağıdaki örnekler geçerli değişken adlarıdır.

```bash
ANAHTAR=değer
_VAR=5
clarus_way=test
```

> Eşittir ( = ) işaretinin her iki tarafında da boşluk olmadığına dikkat edin.

- Aşağıdaki örnekler geçersizdir.

```bash
3_KEY=değer
-VAR=5
clarus yolu=test
KEY_1?=değer1
```

- `?`, `*` veya `-` gibi diğer karakterleri kullanamamamızın nedeni, bu karakterlerin kabuk için özel bir anlamı olmasıdır.

- Yeni bir dosya oluşturun ve onu "variable.sh" olarak adlandırın.

```bash
#!/bin/bash
İSİM=Can
yankı $NAME
```

- Komut dosyasını yürütülebilir yapın ve ardından çalıştırın.

```bash
chmod +x değişken.sh && ./variable.sh
```

### Komut Değiştirme

- Komut ikamesi, bir komutun veya programın (genellikle ekranda yazılacak olan) çıktısını almamızı ve onu bir değişkenin değeri olarak kaydetmemizi sağlar. Bunu yapmak için onu parantez içine koyarız ve ardından bir $ sembolü gelir.

```bash
içerik=$(ls)
yankı $içerik
```

- veya `(backtick) kullanabiliriz

```bash
içerik=`ls`
yankı $içerik
```

- bunu bir senaryoda görelim. Bir dosya oluşturun ve onu "command-substitution.sh" olarak adlandırın.

```bash
#!/bin/bash
çalışma_dizini=$(pwd)
echo "Hoş geldiniz, çalışma dizininiz $working_directory."
```

- Komut dosyasını yürütülebilir yapın ve çalıştırın.

```bash
chmod +x komut ikamesi.sh
./command-substitution.sh
```

- Değişken kullanmadan da aynı sonucu alabiliriz. `command-substitution.sh` dosyasını aşağıdaki gibi güncelleyin.

```bash
#!/bin/bash
echo "Hoş geldiniz, çalışma dizininiz $(pwd)."
echo "Bugün "tarih"
echo "Sen `whoami`sin"
```

- Ve uygula.

```bash
./command-substitution.sh
```

### Konsol girişi

- Bash `read` komutu, kullanıcı girdisi almak için kullanılan güçlü bir yerleşik yardımcı programdır.

- `variable.sh` dosyasını güncelleyin.

```bash
#!/bin/bash
echo "Adınızı giriniz: "
NAME oku
echo "$NAME hoş geldiniz"
```

- Etkileşimli bash betikleri yazarken, kullanıcı girdisini almak için read komutunu kullanabiliriz. Bir bilgi istemi dizesi belirtmek için -p seçeneğini kullanın. Bilgi istemi, okuma yürütülmeden önce yazdırılır ve yeni bir satır içermez.

```bash
read -p "Adınızı giriniz: " İSİM
echo "$NAME hoş geldiniz"
```

- Hassas bilgileri girerken, gelen girişi görüntülemek istemiyoruz. Bunun için `read -s` kullanabiliriz.

```bash
read -p "Adınızı giriniz: " İSİM
echo "$NAME hoş geldiniz"

read -s -p "Şifrenizi giriniz: " ŞİFRE
echo -e "\nŞifreniz $PASSWORD"
```

### Komut Satırı Bağımsız Değişkenleri

- Komut satırı argümanları, İşletim Sistemlerinin komut satırı kabuğunda programın adından sonra verilir. $1, $2, $3, ...$9 komut satırı argümanları konumsal parametrelerdir; $0 gerçek komutu, programı, kabuk betiğini veya işlevi gösterir ve $1, $2, $3, ...$9 emretmek.

- Yeni bir dosya oluşturun ve onu 'argument.sh' olarak adlandırın.

```bash
#!/bin/bash
echo "Dosya Adı $0"
echo "İlk Parametre 1$"
echo "İkinci Parametre 2$"
echo "Üçüncü Parametre 3 Dolar"
echo "Tüm Parametreler $@"
echo "Toplam Parametre Sayısı: $#"
echo "$RANDOM rastgele bir sayıdır"
echo "Geçerli satır numarası $LINENO"
```

- Komut dosyasını yürütülebilir yapın.

```bash
chmod +x argümanı.sh
```

- Aşağıdaki komutla yürütün.

```bash
./argument.sh Joe Matt Timothy James Guile
```

### Diziler

- Programlarımızda, genellikle tek bir değer olarak işlemek için birkaç değeri gruplandırmamız gerekir. Shell'de diziler aynı anda birden fazla değeri tutabilir.

#### Dizileri tanımlama

- Bir dizi değişkeni yaratmanın en basit yöntemi aşağıdadır.

```bash
DISTROS[0]="ubuntu"
DISTROS[1]="fedora"
DISTROS[2]="debian"
DISTROS[3]="centos"
DISTROS[4]="alp"
```

- Aşağıdaki yöntemi de kullanabiliriz.

```bash
devops_tools=("docker" "kubernetes" "ansible" "terraform" "jenkins")
```

#### Dizilerle çalışma

- Bir dizideki bir değere aşağıdaki yöntemi kullanarak ulaşabiliriz.

```bash
yankı ${DİSTRO[0]}
echo ${DAĞITIM[1]}
```

- Sayı yerine `@' koyarak tüm elemanlara ulaşabiliriz.

```bash
echo ${DAĞITIM[@]}
```

- Aşağıdaki yöntemle eleman sayısını öğrenebiliriz.

```bash
echo ${#DISTROS[@]}
```

## Bölüm 3 - Basit Aritmetik

- Bash komut dosyasında aritmetik ifadeyi değerlendirmenin birçok yolu vardır

### ifade

- `expr` komutu, ifadenin değerini standart çıktıya yazdırır. Bunu görelim.

```bash
ifade 3 + 5
ifade 6 - 2
ifade 7 \* 3
ifade 9 / 3
expr 7 % 2
```

- `expr` komutunu kullanarak ifadenin öğeleri arasında boşluk bırakmalı ve ifadenin etrafına tırnak işareti koymamalıyız. Bunu yaparsak, ifade değerlendirilmeyecek, bunun yerine yazdırılacaktır. Farkı gör.

```bash
ifade "3 + 5"
ifade 3-2
```

- Basit bir hesap makinesi oluşturalım. Bir dosya oluşturun ve onu `calculator.sh` olarak adlandırın.

- Komut dosyasını yürütülebilir yapın.

```bash
chmod +x hesap makinesi.sh
```

```bash
#!/bin/bash
read -p "İlk sayıyı girin: " first_number
read -p "İkinci sayıyı girin: " second_number

echo "SUM="`ifade $ilk_sayı + $ikinci_sayı`
echo "SUB="`ifade $ilk_sayı - $ikinci_numara`
echo "MUL="`expr $ilk_numara \* $ikinci_numara`
echo "DIV="`ifade $ilk_sayı / $ikinci_number`
```

> Komut Satırı Argümanları ile nasıl yapabiliriz?

### İzin Vermek

- `let`, basit aritmetik yapmamıza yardımcı olan Bash'in yerleşik bir işlevidir. Cevabı yazdırmak yerine sonucu bir değişkene kaydetmesi dışında 'expr' ile benzerdir. İfadeden farklı olarak, ifadeyi tırnak içine almamız gerekir.

```bash
"toplam = 3 + 5" olsun
yankı $toplam
```

- İfadenin etrafına tırnak işareti koymazsak boşluksuz yazılması gerektiğini unutmayın.

```bash
alt=8-4 olsun
yankı $alt
```

- Ayrıca `let` fonksiyonu ile değişkeni 1 arttırıp azaltabiliriz. Bunu görelim.

```bash
x=5
x++ olsun
yankı $x

y=3
izin ver...
yankı $y
```

- Bir dosya oluşturun ve onu `let-calculator.sh` olarak adlandırın.

```bash
#!/bin/bash
read -p "İlk sayıyı girin: " first_number
read -p "İkinci sayıyı girin: " second_number

"toplam = $birinci_sayı + $ikinci_sayı" olsun
let "alt = $birinci_sayı - $ikinci_sayı"
let "mul = $birinci_sayı * $ikinci_numara"
"div = $birinci_sayı / $ikinci_sayı" olsun
echo "TOPLA=$toplam"
echo "ALT=$alt"
echo "ÇOK=$mul"
echo "BÖL=$div"

ilk_sayı++ olsun
ikinci_sayıya izin ver--
echo "İlk sayının artışı $ilk_sayıdır"
echo "İkinci sayının azalması $saniye_sayıdır"
```

- Komut dosyasını yürütülebilir yapın ve çalıştırın.

```bash
chmod +x let-hesaplayıcı.sh
./let-calculator.sh
```

#### "num++" ve "++num" veya "num--" ve "--num" arasındaki fark

- Bir dosya oluşturun ve onu number.sh olarak adlandırın.

```bash
sayı=10
let new_number=number++ # Bu önce sayıyı atar sonra artar.
echo "Sayı = $sayı"
echo "Yeni sayı = $yeni_numara"

sayı=10
let new_number=--number # Bu önce sayıyı azaltır sonra atar.
echo "Sayı = $sayı"
echo "Yeni sayı = $yeni_numara"
```

- Komut dosyasını yürütülebilir yapın ve çalıştırın.

```bash
chmod +x sayı.sh
./number.sh
```

### Çift Parantez

- Aritmetik ifadeyi çift parantez içinde de değerlendirebiliriz. Bir komutun çıktısını alıp bir değişkenin değeri olarak kaydedebileceğimizi öğrendik. Bu yöntemi temel aritmetik yapmak için kullanabiliriz.

```bash
toplam=$((3 + 5))
yankı $toplam
```

- Aşağıda gördüğümüz gibi, boşluk bırakırsak aynı şekilde çalışır.

```bash
toplam=$((3+5))
yankı $toplam
```

- Bir dosya oluşturun ve onu "parantheses-calculator.sh" olarak adlandırın.

```bash
#!/bin/bash
read -p "İlk sayıyı girin: " first_number
read -p "İkinci sayıyı girin: " second_number

toplam=$(($birinci_sayı + $ikinci_sayı))
alt=$(($birinci_sayı - $ikinci_sayı))
mul=$(($birinci_sayı * $ikinci_sayı))
div=$(($birinci_sayı / $ikinci_sayı))


echo "TOPLA=$toplam"
echo "ALT=$alt"
echo "ÇOK=$mul"
echo "BÖL=$div"

(( ilk_sayı++ ))
(( ikinci_sayı-- ))

echo "İlk sayının artışı $ilk_sayıdır"
echo "İkinci sayının azalması $saniye_sayıdır"
```

- Komut dosyasını yürütülebilir yapın ve çalıştırın.

```bash
chmod +x parantez-hesaplayıcı.sh
./parantheses-calculator.sh
```