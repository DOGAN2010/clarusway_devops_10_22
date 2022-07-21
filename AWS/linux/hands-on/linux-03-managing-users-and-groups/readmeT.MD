# Uygulamalı Linux-03 : Kullanıcıları ve Grupları Yönetme

Bu uygulamalı eğitimin amacı, öğrencilere kullanıcıları ve grupları nasıl yöneteceklerini öğretmektir.

## Öğrenme Çıktıları

Bu uygulamalı eğitimin sonunda öğrenciler;

- linux'ta kullanıcıları ve grupları açıklar.
- kullanıcıları ve grupları yönetin.

## Anahat

- Bölüm 1 - Temel Kullanıcı Komutları

- Bölüm 2 - Kullanıcı Yönetimi

- Bölüm 3 - Kullanıcı Şifreleri

- Bölüm 4 - Grup Yönetimi

## Bölüm 1 - Temel Kullanıcı Komutları
​
- ben kimim.
​
```bash
ben kimim
sudo su
pwd
ben kimim
su ec2 kullanıcısı
sudo su -
pwd
```
​
- kim.
​
```bash
çıkış
kim
who # yeni bir kabuk açıp oturum açan kullanıcıları görmek için who komutunu tekrar deneyin.
```
​
- w.
​
```bash
w
kim
```
​
- kimlik.
​
```bash
İD
kimlik kökü
sudo su
kullanıcı ekle kullanıcı1
kimlik kullanıcısı1
```
​
- su.
​
```bash
su ec2 kullanıcısı
su kullanıcı1
sudo su kullanıcısı1
pwd
çıkış
sudo su - kullanıcı1
pwd
```
​
- şifre.
​
```bash
çıkış
sudo su
kullanıcı ekle kullanıcı2
passwd user2 # user2'ye bir şifre verin
su - kullanıcı2
şifre
çıkış
su kullanıcı2
```
​
## Bölüm 2 - Kullanıcı yönetimi
​
- /etc/passwd.
​
```bash
çıkış
kedi /etc/passwd
tail -3 /etc/passwd
```
​
- useradd.
​
```bash
sudo useradd user3
cd /ev
ls
cd /vb
ls giriş*
kedi oturum açma.defs
sudo nano login.defs # CREATE_HOME değişkeninin değerini "no" olarak değiştirin
sudo useradd user4
cd /ev && ls
kedi /etc/passwd
sudo useradd -m user5 # -m seçeneğiyle kullanıcı için bir giriş dizini oluşturmaya zorla.
cd /ev && ls
sudo useradd -m -d /home/user6home user6 # -d seçeneği ile kullanıcının ana dizini adını değiştirin.
ls
sudo useradd -m -c "bu adam geliştiricidir" user7 # -c seçeneği ile kullanıcıya bir açıklama verir.
kedi /etc/passwd
kedi /etc/passwd | grep kullanıcısı7
```
​
- kullanıcı.
​
```bash
kedi /etc/passwd
sudo kullanıcı kullanıcısı5
kedi /etc/passwd
cd /ev && ls
sudo userdel -r user1 # -r seçeneğiyle kullanıcıyı ve ana dizinini silin.
cd /ev && ls
sudo rm -rf kullanıcı5
```
​
- kullanıcı modu.
​
```bash
kedi /etc/passwd
sudo usermod -c "bu adam bir aws çözüm mimarı olacak" user7
kedi /etc/passwd
sudo usermod --help
sudo usermod -l Superuser user2 # -l seçeneği ile user2'nin adını değiştirin.
kedi /etc/passwd
```
​
## Bölüm 3 - Kullanıcı Şifreleri
​
- passwd-etc/shadow-etc/login.defs.
​
```bash
  sudo su
  kullanıcı ekle kullanıcı8
  şifre kullanıcısı8
  cd /vb
  kedi gölgesi
  kedi oturum açma.defs
```
​
## Bölüm 4 - Grup Yönetimi
​
- gruplar.
​
```bash
gruplar
sudo groupadd linux
sudo groupadd aws
sudo groupadd python
kedi /vb/grup
gruplar
sudo usermod -a -G linux ec2-user # linux grubuna ec2-user ekleyin.
kedi /vb/grup
gruplar
sudo usermod -G aws ec2-user # bu komut, ec2-user varsayılan grubu dışında ec2-user'ın bulunduğu tüm grupları siler ve ec2-user'ı aws grubuna ekler.
kedi /vb/grup
sudo groupmod -n my-linux linux # linux grubunun adını değiştirir.
kedi /vb/grup
gruplar
kedi /vb/grup
sudo groupdel piton
kedi /vb/grup
sudo gpasswd -a user7 aws # bir gruba kullanıcı ekler.
kedi /vb/grup
sudo gpasswd -d user7 aws # bir kullanıcıyı bir gruba siler.
kedi /vb/grup
```