# Uygulamalı EC2-04 : EBS Birimlerini Genişletme ve Bölümleme

Bu uygulamalı eğitimin amacı, öğrencilere bir AWS bulut sunucusuna nasıl EBS (Elastik Blok Depolama) birimi ekleneceğini veya ekleneceğini, birimlerin nasıl genişletileceğini ve yeniden boyutlandırılacağını ve Amazon Linux 2 çalıştıran birimlerde nasıl bölümler oluşturulacağını öğretmektir. EC2 örnekleri.

## Öğrenme Çıktıları

Bu uygulamalı eğitimin sonunda öğrenciler;

- kök hacmi ile EBS Hacmi arasındaki farkın ne olduğunu anlayın.

- birincil (kök) ve ek birimlerin mevcut durumunu göstermek için hacimleri listeleyin

- EBS biriminin nasıl oluşturulacağı konusundaki bilgilerini göstermek.

- EC2 bulut sunucularında montaj noktası oluşturun.

- EC2 bulut sunucularında bölüm hacmi.

- yeni EBS birimlerindeki birimi veya bölümleri yeniden boyutlandırın.

- yeniden başlatmalardan sonra EBS birimlerinin ve bölümlerinin nasıl otomatik olarak monte edileceğini anlayın.

## Anahat

- Bölüm 1 - EBS Birimini Bölümlemeden Genişletin

- Bölüm 2 - Bölümleme ile EBS Birimi Genişletin

- Bölüm 3 - Yeniden Başlatmada EBS Birimlerini ve Bölümlerini Otomatik Olarak Bağlayın

![EBS Birimleri](./ebs_backed_instance.png)

## BÖLÜM 1 - EBS HACİMİNİ BÖLÜMLEMEDEN UZATMA

- "us-east-1a" A'dan Z'ye aws konsolundan bir örnek başlatın.
- örneğe hangi birimlerin eklendiğini kontrol edin.
- sadece kök hacmi listelenmelidir
```
lsblk
```
### Bölüm 0 - Yeni Birim Oluştur

- bu demo için AWS konsolundan "5 GB" örnekle aynı AZ "us-east-1" içinde yeni bir birim oluşturun.
- yeni birimi aws konsolundan ekleyin, ardından blok depolarını tekrar listeleyin.
- kök hacmi ve ikincil hacim listelenmelidir
```
lsblk
```
### Bölüm 1 - Montaj Hacmi

- ekli birimin önceden biçimlendirilip biçimlendirilmediğini ve üzerinde veri olup olmadığını kontrol edin.
```
sudo dosyası -s /dev/xvdf
```
- biçimlendirilmemişse yeni birimi biçimlendirin
```
sudo mkfs -t ext4 /dev/xvdf
```
- biçimlendirmeden sonra birimin biçimini tekrar kontrol edin
```
sudo dosyası -s /dev/xvdf
```
- yeni birim (cilt-1) için bir montaj noktası yolu oluşturun
```
sudo mkdir /mnt/mp1
```
- yeni birimi montaj noktası yoluna monte edin
```
sudo mount /dev/xvdf /mnt/mp1/
```
- bağlı birimin montaj noktası yoluna monte edilip edilmediğini kontrol edin
```
lsblk
```
- montaj noktası yolunda mevcut alanı göster
```
df -h
```
- üzerinde veri olup olmadığını kontrol edin.
```
ls /mnt/mp1/
```
- üzerinde veri yoksa sonraki adımlarda kalıcılığı göstermek için yeni bir dosya oluşturun

```
cd /mnt/mp1
sudo touch merhaba.txt
ls
```
### Bölüm 2: AWS konsolunda yeni birimi (cilt-1) büyütün ve terminalden değiştirin

- aws konsolunda yeni birimi değiştirin ve kapasiteyi 5GB'tan 6GB'a yükseltin.
- ekli birimin yeni kapasiteyi gösterip göstermediğini kontrol edin
```
lsblk
```
- Montaj yolunda kullanılan gerçek kapasiteyi gösterin, eski kapasite gösterilmelidir.
```
df -h
```
- tüm kullanılabilir alanı kapsayacak şekilde yeni birimde dosya sistemini yeniden boyutlandırın.
```
sudo resize2fs /dev/xvdf
```
- şu anda montaj yolunda kullanılan gerçek kapasiteyi gösterin, yeni kapasite, değiştirilmiş hacim boyutunu yansıtmalıdır.
```
df -h
```
- verilerin yeni büyütülmüş birimde hala devam ettiğini gösterin.
```
ls /mnt/mp1/
```
## Bölüm 3: Örneği Yeniden Başlatma

- örnek yeniden başlatıldığında montaj noktası yolunun kaybolacağını göster
```
sudo şimdi yeniden başlat
```
- yeni birimin hala takılı olduğunu, ancak takılı olmadığını gösterin
```
lsblk
```
- ekli birimin "zaten biçimlendirilmiş" olup olmadığını ve üzerinde veri olup olmadığını kontrol edin.
```
sudo dosyası -s /dev/xvdf
```
- yeni birimi montaj noktası yoluna monte edin
```
sudo mount /dev/xvdf /mnt/mp1/
```
- kullanılan ve kullanılabilir kapasitenin disk boyutuyla aynı olduğunu gösterin.
```
lsblk
df -h
```
- üzerinde veri varsa, verinin hala devam edip etmediğini kontrol edin.
```
ls /mnt/mp1/
```

## BÖLÜM 2 - BÖLÜMLEMEYLE EBS HACİMİNİ UZATIN

- https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/recognize-expanded-volume-linux.html

- https://www.tecmint.com/fdisk-commands-to-manage-linux-disk-partitions/

- mevcut durumu göstermek için liste hacimleri, birincil (kök) ve ikincil hacimler listelenmelidir
```
lsblk
```
- hacimlerle ilgili kullanılan ve mevcut kapasiteleri göster
```
df -h
```
### Bölüm 0: Yeni birim oluştur

- aws konsolundaki örnekle aynı AZ "us-east-1" içinde üçüncül birim (bu demo için 5 GB) oluşturun
- yeni birimi aws konsolundan ekleyin, ardından birimleri tekrar listeleyin.
- birincil (kök), ikincil ve üçüncül birimler listelenmelidir
```
lsblk
```
- hacimlerle ilgili kullanılan ve mevcut kapasiteleri göster
```
df -h
```
- mevcut bölümleri göster ... belirli bölüm için "fdisk -l /dev/xvda" kullanın
```
sudo fdisk -l
```

### Bölüm 1: Bölüm-1'i yapın

- mevcut tüm fdisk komutlarını kontrol edin ve "m" kullanarak.

```
sudo fdisk /dev/xvdg

 n -> yeni bölüm ekle (1G boyutunda)
 p -> birincil
 Bölüm numarası: 1
 Birinci sektör: varsayılan - varsayılanı seçmek için Enter'ı kullanın
 Son sektör: +2G
  
 
 n -> yeni bölüm ekle (boy-1G'nin geri kalanıyla)
 p -> birincil
 Bölüm numarası: 2
 Birinci sektör: varsayılan - varsayılanı seçmek için Enter'ı kullanın
 Son sektör: varsayılan - varsayılanı seçmek için Enter'ı kullanın
 w -> bölüm tablosu yaz
 
 ```
- yeni bölümleri biçimlendirin
```
sudo mkfs -t ext4 /dev/xvdg1
sudo mkfs -t ext4 /dev/xvdg2
```
- yeni birim için bir montaj noktası yolu oluşturun
```
sudo mkdir /mnt/mp2
sudo mkdir /mnt/mp3
```
- yeni birimi montaj noktası yoluna monte edin
```
sudo mount /dev/xvdg1 /mnt/mp2/
sudo mount /dev/xvdg2 /mnt/mp3/
```
- mevcut durumu göstermek için liste hacimleri, tüm ciltler ve bölümler listelenmelidir
```
lsblk
```
- hacimler ve bölümlerle ilgili kullanılan ve mevcut kapasiteleri gösterin
```
df -h
```

- üzerinde veri yoksa sonraki adımlarda kalıcılığı göstermek için yeni bir dosya oluşturun
```
sudo touch /mnt/mp3/helloguys.txt
ls /mnt/mp3/
```
### Bölüm 3: Kapasiteyi büyüt

- aws konsolundaki yeni (3.) birimi değiştirin ve kapasiteyi 1 GB daha artırın (bu demo için 5 GB'den 6 GB'a).
- ekli birimin yeni kapasiteyi gösterip göstermediğini kontrol edin
```
lsblk
```
- Montaj yolunda kullanılan gerçek kapasiteyi gösterin, eski kapasite gösterilmelidir.
```
df -h
```
- 2. bölümü genişletin ve yeni kullanılabilir tüm alanı işgal edin. Uzay için uyarı !!!!!!
```
sudo büyüme bölümü /dev/xvdg 2
```
- Montaj yolunda kullanılan gerçek kapasiteyi göster, güncel kapasite gösterilmelidir.
```
lsblk
```
- DOSYA Sistemini yeniden boyutlandırın ve genişletin.
```
sudo resize2fs /dev/xvdg2
```
- kalıcılığı göstermek için yeni oluşturulan dosyayı göster

```
ls /mnt/mp3/
```
- yeniden başlatın ve yapılandırmanın gittiğini gösterin
```
sudo şimdi yeniden başlat
```


## BÖLÜM 3 - YENİDEN BAŞLATMADAKİ EBS BİRİMLERİNİ VE BÖLÜMLERİ AUTOMONT

- /etc/fstab dosyasını yedekleyin.
```
sudo cp /etc/fstab /etc/fstab.bak
```
- /etc/fstab dosyasını açın ve

```
sudo nano /etc/fstab
```
- mevcut olana aşağıdaki bilgileri ekleyin.(UUID'ler de kullanılabilir)
```
 /dev/xvdf mnt/mp1 ext4 varsayılanları,başarısız 0 0
 /dev/xvdg1 mnt/mp2 ext4 varsayılanları,başarısız 0 0
 /dev/xvdg2 mnt/mp3 ext4 varsayılanları,başarısız 0 0
```
 

- yeniden başlatın ve yapılandırmanın var olduğunu gösterin (NOT)
```
sudo şimdi yeniden başlat
```
- mevcut durumu göstermek için liste hacimleri, tüm ciltler ve bölümler listelenmelidir
```
lsblk
```
- hacimler ve bölümlerle ilgili kullanılan ve mevcut kapasiteleri gösterin
```
df -h
```
- üzerinde veri varsa, verinin hala devam edip etmediğini kontrol edin.
```
ls /mnt/mp1/
ls /mnt/mp3/
```

# NOT: Yeniden başlatmadan fstab dosyasını düzenledikten sonra birimleri ve bölümleri monte etmek için "sudo mount -a" kullanabilirsiniz.
