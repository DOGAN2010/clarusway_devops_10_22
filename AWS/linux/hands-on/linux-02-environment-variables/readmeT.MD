# Hands-on Linux-02 : Linux Environment Variables

Bu uygulamalı eğitimin amacı, öğrencilere ortam değişkenlerini nasıl kullanacaklarını öğretmektir.

## Öğrenme Çıktıları

Bu uygulamalı eğitimin sonunda öğrenciler;

- ortam değişkenlerini açıklar.

- Değişkenlerle Alıntı Yapmayı anlayın.

## Anahat

- Bölüm 1 - Ortak Ortam Değişkenleri ve Değişkene Erişme

- Bölüm 2 - Yol Değişkeni

- Bölüm 3 - Değişkenlerle Alıntı Yapma

- Bölüm 4 - Sudo Komutu

## Bölüm 1 - Ortak Ortam/Kabuk Değişkenleri ve Değişkene Erişme
​
- "env" ve "printenv" komutları arasındaki fark.
​
```bash
ortam
printenv
printenv ANA SAYFA
yankı $HOME
env ANASAYFA
```
​
- Kabuk değişkenini anlama.
​
```bash
CLARUS=yol
ortam
Ayarlamak
ayarla | grep CLARUS
yankı $CLARUS
```
​
- Ortam değişkenini anlama. Dışa aktarma komutunu kullanın.
​
```bash
dışa aktarma YOLU=clarus
ortam
```
​
- Kabuk ve ortam değişkenleri arasındaki fark. Bir kullanıcı oluşturun, "user1" olarak adlandırın, user1'e geçin, ortamı ve kabuk değişkenlerini kontrol edin.
​
```bash
dışa aktarma YOLU=clarus
sudo su
kullanıcı ekle kullanıcı1
passwd user1 # user1'e herhangi bir şifre verin.
çıkış
su kullanıcı1
çevre | grep YOLU
ayarla | grep CLARUS
```
​
- Ortam değişkeni değerini değiştirin.
​
```bash
dışa aktarma YOLU=linux
ortam
dışa aktarma YOLU=komut dosyası
ortam
```
​
- unset komutuyla ortam değişkenini kaldırın.
​
```bash
dışa aktarma YOLU=clarusway
çevre | grep YOLU
YOL ayarını kaldır
çevre | grep YOLU
```
​
## Bölüm 2 - Yol Değişkeni
​
- YOL değişkeni.
​
```bash
printenv YOL
cd / kutu
ls ca* # cat komutuna bakın.
```
​
- Bir komut dosyasını çalıştırmak için PATH değişkenine bir yol ekleyin.
​
```bash
CD
mkdir testi && cd testi
nano test.sh
# "merhaba dünya" kodunu kopyalayıp test.sh içine yapıştırın
chmod +x testi.sh
./test.sh
cd # dizini ec2 kullanıcısının ana dizinine değiştir
./test.sh # çalışmıyor.
./test/test.sh
printenv YOL
cd testi
pwd
dışa aktar YOL=$YOL:/home/ec2-user/test
printenv YOL
CD
test.sh
cd /
test.sh
```
​
- Komut dosyasında ortam değişkenini kullanma.
​
```bash
cd testi
dışa aktar CLARUS=env.var
YOL=kabuk.var
cd testi
nano test1.sh
# kod yankısını kopyalayıp yapıştırın "normalde $CLARUS env. değişkenini görmeliyiz ama muhtemelen $WAY kabuk değişkenini göremiyoruz "
chmod +x test1.sh
./test1.sh
```
​
## Bölüm 3 - Değişkenlerle Alıntı Yapma.
​
- İkili alıntı.
​
```bash
MYVAR=benim değerim
yankı $MYVAR
MYVAR="değerim"
yankı $MYVAR
BENİM ADIM=james
MYVAR="adım $MYNAME"
yankı $MYVAR
BENİM ADI="james"
MYVAR="merhaba $MYNAME"
yankı $MYVAR
MYVAR="merhaba \$MYNAME"
yankı $MYVAR
```
​
- Tek Alıntılar.
​
```bash
echo '$ KABUK'
echo 'Benim\$KABUĞUM'
```
​
## Bölüm 4 - Sudo Komutu.
​
- Sudo Komutanlığı.
​
```bash
yum güncellemesi
sudo yum güncellemesi
cd /
mkdir test dosyası
sudo su
sudo -s
sudo su -
```