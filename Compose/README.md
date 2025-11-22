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
