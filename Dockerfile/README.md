🐳 **Dockerfile Nedir?**

Dockerfile, bir Docker imajını oluşturmak için kullanılan metin tabanlı talimat dosyasıdır.
Her satır, imajın nasıl inşa edileceğini ve container çalıştırıldığında ne yapacağını belirler.


| Komut     | Açıklama                                    |
| --------- | ------------------------------------------- |
| `FROM`    | Hangi temel imajdan başlanacağını belirler  |
| `RUN`     | Container içinde komut çalıştırır           |
| `COPY`    | Dosyaları host’tan container’a kopyalar     |
| `WORKDIR` | Çalışma dizinini ayarlar                    |
| `EXPOSE`  | Container’ın açacağı port                   |
| `CMD`     | Container çalıştırıldığında çalışacak komut |
