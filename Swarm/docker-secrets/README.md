Uygulama Örneği (PostgreSQL Şifresi)
Şimdi, bir veritabanı (örneğin PostgreSQL) servisine şifresini Secret olarak atayan bir örnek yapalım.

Adım 1: Secret'ı Yaratmak
Önce, veritabanı için kullanacağımız şifreyi içeren bir Secret oluşturalım.

Şifre Dosyasını Oluşturun: Basitçe, bir dosyaya şifrenizi yazın. İçinde sadece şifreniz olmalı (Örn: mYSuPeRgIzLiPasSwOrD123).

Bash

echo "mYSuPeRgIzLiPasSwOrD123" > db_password.txt
Secret'ı Docker'a Yükleyin: Bu dosyayı kullanarak Secret'ı oluşturuyoruz. Secret'ın adı postgres_root_password olacak.

Bash

docker secret create postgres_root_password db_password.txt
Çıktı: Docker size uzun bir ID verecektir. Bu, Secret'ın başarılı bir şekilde oluşturulduğu anlamına gelir.

Bash

# Örn:
# y3l2s1z0b8n6p4m0r5q3d2c1a0t9u7
Şimdi bu hassas bilgi, Swarm içinde güvenli bir şekilde saklanıyor. Artık db_password.txt dosyasını silebilirsiniz.


Adım 2: Stack Dosyasını Hazırlamak
stack-demo-secrets.yml adında yeni bir dosya oluşturalım ve bu Secret'ı nasıl kullanacağımızı gösterelim.



Adım 3: Stack'i Dağıtmak ve Kontrol Etmek
Stack'i dağıtalım:

Bash

docker stack deploy -c stack-demo-secrets.yml gizli-projem
Uygulama container'ının içine gidip Secret'ın doğru yerleştirilip yerleştirilmediğini kontrol edelim:

Uygulama servisi içindeki container ID'sini bulun:

Bash

docker ps -f name=gizli-projem_app
# Örn: Container ID: e9f0a1b2c3
Container'ın dosya sistemini kontrol edin:

Bash

docker exec <CONTAINER_ID> ls -l /run/secrets
Çıktı:

total 4
-r--r--r--    1 root     root             27 Nov 26 13:00 postgres_root_password
Gördüğünüz gibi, Secret'ın adında bir dosya oluşmuş! Uygulamanız bu dosyayı okuyarak şifreyi alabilir.

3. Temizlik
İşlem bitince oluşturduğunuz her şeyi silin:

Bash

docker stack rm gizli-projem
docker secret rm postgres_root_password
docker swarm leave --force