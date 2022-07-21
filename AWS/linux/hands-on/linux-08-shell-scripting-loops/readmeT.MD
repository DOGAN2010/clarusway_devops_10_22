# Uygulamalı Linux-07 : Kabuk Komut Dosyası/Koşullu İfadeler

Bu uygulamalı eğitimin amacı, öğrencilere kabukta koşullu ifadelerin nasıl kullanılacağını öğretmektir.

## Öğrenme Çıktıları

Bu uygulamalı eğitimin sonunda öğrenciler;

- Shell'de koşullu ifadeleri açıklayın.

- kabuk komut dosyasında if ifadelerini kullanın

- kabuk komut dosyasında vaka ifadelerini kullanın

## Anahat

- Bölüm 1 - If İfadeleri

- Bölüm 2 - If Else İfadeleri

- Bölüm 3 - Elif Else İfadeleri Varsa

- Bölüm 4 - İç İçe If İfadeleri

- Bölüm 5 - Boole İşlemleri

- Bölüm 6- Vaka Açıklamaları

## Bölüm 1 - If İfadeleri

- Unix Shell, farklı koşullar temelinde farklı eylemler gerçekleştirmek için kullanılan koşullu ifadeleri destekler.

- Basit bir if ifadesi, esasen, belirli bir testin doğru olup olmadığını, ardından belirli bir dizi eylemi gerçekleştirdiğini belirtir. Doğru değilse, bu eylemleri yapmayın.

- Bir klasör oluşturun ve onu "koşullu ifadeler" olarak adlandırın.

```bash
mkdir koşullu ifadeler && cd koşullu ifadeler
```

- 'if-statement.sh' adlı bir 'script' dosyası oluşturun.

```bash
#!/bin/bash
read -p "Bir sayı girin: " sayı

eğer [[ $sayı -gt 50 ]]
sonra
  echo "Sayı büyük."
fi
```

- Komut dosyasını yürütülebilir yapın ve çalıştırın.

```bash
chmod +x if-deyimi.sh
./if-statement.sh
```

- Yukarıdaki if ifadesinde köşeli parantezler ( [ ] ) içinde `İlişkisel İşleçler`, `Dize İşleçleri` veya `Dosya Test Operatörleri` kullanabiliriz.

### İlişkisel Operatörler

- Bourne Shell, aşağıdaki sayısal değerlere özgü ilişkisel işleçleri destekler. Bu operatörler, dize değerleri için çalışmaz.

| Operatör | Açıklama |
| -------- | ----------- |
| -eq | eşit |
| -ne | eşit değil |
| -gt | daha büyük |
| -lt | daha az |
| -ge | büyük veya eşit |
| -le | küçük veya eşit |

### Dizi Operatörleri

- Aşağıdaki dize operatörleri Bourne Shell tarafından desteklenmektedir.

| Operatör | Açıklama |
| -------- | ----------- |
| = | eşit |
| != | eşit değil |
| -z | Boş dize |
| -n | Boş dize değil |

- Şuna bir bakalım. Bir dosya oluşturun ve onu "string-operators.sh" olarak adlandırın

```bash
#!/bin/bash

eğer [[ "a" = "a" ]]
sonra
  echo "Onlar aynı"
fi

if [[ "a" != "b" ]]
sonra
  echo "Aynı değiller"
fi

eğer [[ -z "" ]]
sonra
  echo "Boş"
fi

eğer [[ -n "metin" ]]
sonra
  echo "Boş değil"
fi
```

- Açılış ayracı `[` ile "metin" = "metin" parametreleri arasında ve ardından parametreler ile kapanış ayracı `]` arasında boşluk olduğuna dikkat edin. Bunun nedeni tam olarak buradaki parantezlerin bir komut görevi görmesi ve sizin komutu parametrelerinden ayırmanızdır.

- Komut dosyasını yürütülebilir yapın ve çalıştırın.

```bash
chmod +x string-operators.sh
./string-operators.sh
```

### Dosya Test Operatörleri

- Bir Linux dosyasıyla ilişkili çeşitli özellikleri test etmek için kullanılabilecek birkaç operatör vardır.

| Operatör | Açıklama |
| -------- | ----------- |
| -d dosyası | dizin |
| -e dosyası | var |
| -f dosyası | sıradan dosya |
| -r dosyası | okunabilir |
| -s dosyası | boyut > 0 bayt |
| -w dosyası | yazılabilir |
| -x DOSYA | yürütülebilir |

- Hadi bunu deneyelim. Aşağıdaki dosyaları oluşturun ve yapılandırın.

```bash
mkdir klasörü
dokunmatik dosya
chmod 400 dosyası
```

Bir dosya oluşturun ve onu `file-operators.sh` olarak adlandırın

```bash
#!/bin/bash

eğer [[ -d klasörü ]]
sonra
  echo "klasör bir dizindir"
fi

eğer [[ -f dosyası ]]
sonra
  echo "dosya sıradan bir dosyadır"
fi

eğer [[ -r dosyası ]]
sonra
  echo "dosya okunabilir bir dosyadır"
fi

eğer [[ -w dosyası ]]
sonra
  echo "dosya yazılabilir bir dosyadır"
fi

eğer [[ -s dosyası ]]
sonra
  echo "dosya > 0 bayttır"
fi

eğer [[ -x $0 ]]
sonra
  echo "$0 yürütülebilir bir dosyadır"
fi
```

- Komut dosyasını yürütülebilir yapın ve çalıştırın.

```bash
chmod +x file-operators.sh
./file-operators.sh
```

## 2. Kısım - If Else İfadeleri

- Bazen bir ifade doğruysa bir kod bloğunu, yanlışsa başka bir kod bloğunu yürütmek isteriz.

- 'ifelse-statement.sh' adlı bir 'script' dosyası oluşturun.

```bash
#!/bin/bash
read -p "Bir sayı girin: " sayı

eğer [[ $sayı -ge 10 ]]
sonra
  echo "Sayı 10'dan büyük veya 10'a eşit."
Başka
  echo "Sayı 10'dan küçük"
fi
```

- Komut dosyasını yürütülebilir yapın ve çalıştırın.

```bash
chmod +x ifelse-deyimi.sh
./ifelse-statement.sh
```

> - Bir komut dosyası oluşturun. Kullanıcıdan oluşturmak için bir "dosya adı" girmesini isteyin.
> - Aynı ada sahip bir dosya varsa, "Dosya zaten var" mesajını yazdırın.
> - Değilse, dosyayı oluşturun ve "Dosya oluşturuldu" mesajını yazdırın.

## Bölüm 3 - Eğer Elif Else İfadeleri

- Elif deyimi, programımızda birden fazla koşulun belirtilmesi gerektiğinde kullanılır.

- 'elif-statement.sh' adında bir 'script' dosyası oluşturun.

```bash
#!/bin/bash
read -p "Bir sayı girin: " sayı

eğer [[ $sayı -eq 10 ]]
sonra
  echo "Sayı 10'a eşittir."
elif [[ $sayı -gt 10 ]]
sonra
  echo "Sayı 10'dan büyük"
Başka
  echo "Sayı 10'dan küçük"
```

- Komut dosyasını yürütülebilir yapın ve çalıştırın.

```bash
chmod +x elif-ifadesi.sh
./elif-statement.sh
```

## Bölüm 4 - İç İçe If İfadeleri

- If ifadeleri iç içe yerleştirilebilir. Aşağıdaki örnekte yuvalanmış yapıyı görelim.

- "nested-if-statement.sh" adlı bir "komut dosyası" dosyası oluşturun.

```bash
#!/bin/bash

read -p "Bir sayı girin: " sayı

eğer [[ $sayı -gt 10 ]]
sonra
  echo "Sayı 10'dan büyük"

  if (( $sayı % 2 == 1 ))
  sonra
    echo "Ve tek bir sayıdır."
  Başka
    echo "Ve çift sayıdır"
  fi
Başka
  echo "10'dan büyük değil"
fi
```

- Komut dosyasını yürütülebilir yapın ve çalıştırın.

```bash
chmod +x iç içe-if-deyimi.sh
./nested-if-statement.sh
```

## Bölüm 5 - Boole İşlemleri

- Aşağıdaki Boole operatörleri Bourne Shell tarafından desteklenmektedir.

| Operatör | Açıklama |
| -------- | ----------- |
| ! | olumsuzlama |
| && | ve |
| || | veya |

- `!` doğru bir koşulu yanlışa çevirir ve bunun tersi de geçerlidir.

- `&&` mantıklı VE'dir. Her iki işlenen de doğruysa, koşul doğru olur, aksi halde yanlış olur.

- `||` mantıksal VEYA'dır. İşlenenlerden biri doğruysa, koşul doğru olur.

- "boolean.sh" adında bir "komut dosyası" dosyası oluşturun.

```bash
#!/bin/bash

read -p "Adınızı girin: " name
read -sp "Şifrenizi girin: " şifre

if [[ $isim = $(whoami) ]] && [[ $şifre = Aa1234 ]]
sonra
  echo -e "\nHoş geldiniz $(whoami)"
Başka
  echo -e "\nYanlış hesap"
fi
```

- Komut dosyasını yürütülebilir yapın ve çalıştırın.

```bash
chmod +x boolean.sh
./boolean.sh
```

## Bölüm 6- Vaka Açıklamaları

- Çok yollu bir dal yürütmek için birkaç if-elif deyimi kullanabiliriz, ancak bu kısa sürede karmaşık hale gelecektir. Bash durum ifadeleri, if-else ifadelerine benzer ancak daha kolay ve basittir. Bir değişkeni birkaç değerle eşleştirmeye yardımcı olur.

- 'case-statement.sh' adında bir 'script' dosyası oluşturun.

```bash
#!/bin/bash

read -p "İlk sayıyı girin: " first_number
read -p "İkinci sayıyı girin: " second_number
read -p "Bir matematik işlemi seçin
1 - ekleme
2 - çıkarma
3 - çarpma
4 - bölme
" operasyon

durumda $operasyon
  "1")
     echo "sonuç= $(( $birinci_sayı + $ikinci_sayı))"
  ;;
  "2")
     echo "sonuç= $(( $birinci_sayı - $ikinci_sayı))"
  ;;
  "3")
     echo "sonuç= $(( $birinci_sayı * $ikinci_sayı))"
     ;;
  "4")
     echo "sonuç= $(( $ilk_sayı / $ikinci_number))"
  ;;
  *)
     echo "Yanlış seçim..."
  ;;
esac
```

- Komut dosyasını yürütülebilir yapın ve çalıştırın.

```bash
chmod +x case-statement.sh
./case-statement.sh
```