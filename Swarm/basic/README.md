Adım 1: Tek Kişilik Orduyu Kur (Swarm Init)
Mevcut bilgisayarını Swarm Yöneticisi (Manager) ilan edelim.

Bash

docker swarm init

Adım 2: İlk Servisini Yarat (Merhaba Docker!)
Standart nginx sunucusunu bir servis olarak başlatalım. Çakışma olmaması için 8080 portunu kullanalım.

Bash

docker service create --name web-sitem -p 8080:80 nginx
Şimdi tarayıcını açıp http://localhost:8080 adresine git. "Welcome to nginx!" yazısını gördün mü? Süper, servis çalışıyor.


Adım 3: Çoğaltma Zamanı (Scaling)
Şu an 1 tane container çalışıyor. Diyelim ki sitene binlerce kişi girdi. Tek komutla sunucu sayısını 5'e çıkaralım.

Bash

docker service scale web-sitem=5
Şimdi gerçekten 5 tane olup olmadığına bakalım:

Bash

docker service ps web-sitem
Ekranda 5 satır göreceksin. Running statüsünde 5 farklı container emrine amade.

Adım 4: Dayanıklılık Testi (Kaos Yaratma!)
Docker Swarm'ın en havalı özelliği olan "Self-Healing" (Kendini İyileştirme) özelliğini test edelim. Docker, biz 5 tane istediğimiz için o sayıyı ne pahasına olursa olsun koruyacak.

Önce çalışan containerlardan birinin ID'sini bulup not edelim (veya kopyalayalım):

Bash

docker ps
(Listeden rastgele bir nginx container ID'si seç, örneğin a1b2c3d4)

Şimdi o container'ı zorla öldür (sanki sunucu çökmüş gibi):

Bash

docker rm -f <KOPYALADIGIN_CONTAINER_ID>
Hemen (birkaç saniye içinde) servis durumuna tekrar bak:

Bash

docker service ps web-sitem
Ne Göreceksin? Listede eski container için "Shutdown" veya "Failed" yazdığını, ancak hemen üstünde yepyeni bir container'ın pırıl pırıl çalışmaya başladığını göreceksin. Swarm, eksilen askerin yerine hemen yenisini koydu.

Adım 5: Temizlik (Parti Bitti)
Denemeyi bitirdiğinde bilgisayarını eski haline döndürmek için önce servisi sil, sonra Swarm modundan çık.

Bash

docker service rm web-sitem
docker swarm leave --force
Nasıl buldun? Özellikle bir container'ı sildiğinde Swarm'ın onu otomatik olarak geri getirmesi, üretim ortamlarında (production) "gece rahat uyumanı" sağlayan özelliktir.