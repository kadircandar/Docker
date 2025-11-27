# Docker Secrets ile PostgreSQL Şifresi Yönetimi

Bir veritabanı (PostgreSQL) servisine şifresini güvenli bir şekilde Secret olarak atama rehberi.

## Adım 1: Secret'ı Yaratmak

Önce, veritabanı için kullanacağımız şifreyi içeren bir Secret oluşturalım.

### 1.1 Şifre Dosyasını Oluşturun

Basitçe, bir dosyaya şifrenizi yazın. İçinde sadece şifreniz olmalı (Örn: `mYSuPeRgIzLiPasSwOrD123`).

```bash
echo "mYSuPeRgIzLiPasSwOrD123" > db_password.txt
```

### 1.2 Secret'ı Docker'a Yükleyin

Bu dosyayı kullanarak Secret'ı oluşturuyoruz. Secret'ın adı `postgres_root_password` olacak.

```bash
docker secret create postgres_root_password db_password.txt
```

**Çıktı:** Docker size uzun bir ID verecektir. Bu, Secret'ın başarılı bir şekilde oluşturulduğu anlamına gelir.

```bash
# Örnek çıktı:
# y3l2s1z0b8n6p4m0r5q3d2c1a0t9u7
```

> 🔒 **Güvenlik Notu:** Şimdi bu hassas bilgi, Swarm içinde güvenli bir şekilde saklanıyor. Artık `db_password.txt` dosyasını silebilirsiniz.

## Adım 2: Stack Dosyasını Hazırlamak

`stack-demo-secrets.yml` adında yeni bir dosya oluşturalım ve bu Secret'ı nasıl kullanacağımızı gösterelim.

```yaml
version: '3.8'

services:
  app:
    image: alpine:latest
    command: sleep 3600
    secrets:
      - postgres_root_password

secrets:
  postgres_root_password:
    external: true
```

## Adım 3: Stack'i Dağıtmak ve Kontrol Etmek

### 3.1 Stack'i Dağıtalım

```bash
docker stack deploy -c stack-demo-secrets.yml gizli-projem
```

### 3.2 Secret'ı Kontrol Edelim

Uygulama container'ının içine gidip Secret'ın doğru yerleştirilip yerleştirilmediğini kontrol edelim.

**Container ID'sini bulun:**

```bash
docker ps -f name=gizli-projem_app
# Örnek çıktı: Container ID: e9f0a1b2c3
```

**Container'ın dosya sistemini kontrol edin:**

```bash
docker exec <CONTAINER_ID> ls -l /run/secrets
```

**Beklenen Çıktı:**

```
total 4
-r--r--r--    1 root     root             27 Nov 26 13:00 postgres_root_password
```

> ✅ **Başarılı!** Gördüğünüz gibi, Secret'ın adında bir dosya oluşmuş! Uygulamanız bu dosyayı okuyarak şifreyi alabilir.

### 3.3 Secret İçeriğini Okumak (Opsiyonel)

Secret'ın içeriğini görmek için:

```bash
docker exec <CONTAINER_ID> cat /run/secrets/postgres_root_password
```

## Adım 4: Temizlik

İşlem bitince oluşturduğunuz her şeyi silin:

```bash
docker stack rm gizli-projem
docker secret rm postgres_root_password
docker swarm leave --force
```

---

## Özet

Docker Secrets ile:
- 🔐 Hassas bilgiler güvenli bir şekilde saklanır
- 📂 Secret'lar `/run/secrets/` dizininde dosya olarak mount edilir
- 🔒 Container'lar yalnızca kendilerine atanan Secret'lara erişebilir
- 🚀 Production ortamında güvenli şifre yönetimi sağlanır

## Gerçek Dünya Örneği: PostgreSQL

PostgreSQL ile kullanım örneği:

```yaml
version: '3.8'

services:
  db:
    image: postgres:15
    secrets:
      - postgres_root_password
    environment:
      POSTGRES_PASSWORD_FILE: /run/secrets/postgres_root_password
    deploy:
      replicas: 1

secrets:
  postgres_root_password:
    external: true
```

Bu yapılandırma ile PostgreSQL, şifreyi `/run/secrets/postgres_root_password` dosyasından okuyarak başlatılır. 🎯
