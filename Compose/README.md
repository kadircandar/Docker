🐳 **Docker Compose Nedir?**

Docker Compose, birden fazla Docker container'ını (örneğin; Web sunucusu + Veritabanı + Redis) tek bir dosya üzerinden tanımlayıp, tek bir komutla yönetmenizi sağlayan bir araçtır.

Bunu bir **Orkestra Şefi** gibi düşünebilirsiniz:
- **Docker:** Tek bir müzisyendir (tek bir container çalıştırır).
- **Docker Compose:** Orkestra şefidir. Hangi müzisyenin ne zaman çalacağını, kiminle uyum içinde olacağını (network) ve notalarını (konfigürasyon) yönetir.


## 🛠️ Sık Kullanılan Komutlar (Cheat Sheet)

Docker Compose ile çalışirken işinize yarayacak temel komutlar:

| Komut | Açıklama |
| :--- | :--- |
| `docker-compose up -d` | Servisleri arka planda başlatır. |
| `docker-compose down` | Servisleri durdurur ve container'ları siler. |
| `docker-compose down -v` | Servisleri durdurur ve **verileri (volume)** de siler. |
| `docker-compose logs -f` | Logları canlı olarak ekrana basar. |
| `docker-compose ps` | Çalışan servislerin durumunu gösterir. |
| `docker-compose restart` | Servisleri yeniden başlatır. |



Harika, docker-compose.yml dosyası aslında bir "reçete" gibidir. İçindeki her bir satır, Docker'a o yemeği (uygulamayı) nasıl pişireceğini anlatır.

İşte bir Compose dosyasında en sık karşılaşılan anahtar kelimeler ve ne işe yaradıkları:
## 📄 Docker Compose Dosya Yapısı

Aşağıda, `docker-compose.yml` dosyası içinde kullanılan temel komutların açıklamaları yer almaktadır:

| Komut | Ne İşe Yarar? | Örnek Kullanım |
| :--- | :--- | :--- |
| **`version`** | Compose dosyasının sürümünü belirtir. | `version: '3.8'` |
| **`services`** | Çalıştırılacak uygulamaların (container) listelendiği ana bloktur. | `services:` |
| **`image`** | Container'ın oluşturulacağı imajı belirtir. | `image: elasticsearch:7.17` |
| **`container_name`** | Container'a özel bir isim verir. | `container_name: my_db` |
| **`ports`** | Dış dünya ile container arasındaki port yönlendirmesini yapar. | `ports: - "5601:5601"` |
| **`environment`** | Uygulamanın çalışması için gerekli ortam değişkenlerini (env vars) tanımlar. | `discovery.type=single-node` |
| **`volumes`** | Verilerin kalıcı olması için disk alanı tanımlar. | `volumes: - db_data:/var/lib/mysql` |
| **`depends_on`** | Servislerin başlama sırasını belirler. | `depends_on: - elasticsearch` |
| **`restart`** | Hata durumunda container'ın ne yapacağını belirler. | `restart: always` |
| **`networks`** | Container'ların haberleşeceği özel ağı tanımlar. | `networks: - elk_net` |


