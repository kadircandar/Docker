🐳 **Docker Swarm Nedir?**

Docker Swarm, birden fazla Docker makinesini tek bir sanal sistemmiş gibi yönetmenizi sağlayan yerleşik bir orkestrasyon aracıdır.


**1. Temel Kavramlar**

- **Node (Düğüm):** Swarm kümesine dahil olan her bir sunucu veya bilgisayardır.
- **Manager Node (Yönetici Düğüm):** Swarm kümesini yöneten ve görev dağıtımını kontrol eden düğümdür.
- **Worker Node (İşçi Düğüm):** Yönetici düğüm tarafından atanan görevleri yerine getiren düğümdür.
- **Service (Servis):** Swarm üzerinde çalışan uygulama bileşenleridir.
- **Task (Görev):** Bir servisin çalıştırdığı container örneğidir.

**Docker Stack:** Docker Swarm üzerinde birden fazla servisi tek bir yığın (stack) olarak yönetmenizi sağlar. Bu, uygulamalarınızı daha kolay dağıtmanıza ve ölçeklendirmenize olanak tanır.

**Neden Stack Kullanıyoruz?**
 - **Belgeleme:** stack.yml dosyası artık projenin bir belgesi oldu. "Bu sistemde ne çalışıyor?" sorusunun cevabı dosyada yazılı.
 - **Versiyon Kontrolü:** Bu dosyayı Git gibi sistemlerde saklayabilir, değişiklikleri takip edebilirsin.
 - **Kolaylık:** 50 tane servisi tek komutla (docker stack deploy) başlatabilir veya güncelleyebilirsin.

**Docker Secrets**: Swarm ortamında hassas bilgileri (şifreler, API anahtarları vb.) güvenli bir şekilde yönetmenizi sağlar.

<br>&nbsp;<br>

| Komut                        | Açıklama                                                         |
| ---------------------------- | ---------------------------------------------------------------- |
| `docker swarm init`          | Swarm modunu başlatır ve bu makineyi bir swarm yöneticisi yapar  |
| `docker swarm join`          | Bir makineyi mevcut bir swarm'a katılmasını sağlar               |
| `docker service create`      | Swarm üzerinde yeni bir servis oluşturur                         |
| `docker service ls`          | Swarm üzerindeki servisleri listeler                             |
| `docker service scale`       | Servislerin replika sayısını artırır/azaltır                     |
| `docker service rm`          | Swarm üzerindeki bir servisi siler                               |
| `docker node ls`             | Swarm üzerindeki düğümleri listeler                              |
| `docker swarm leave`         | Makinenin swarm'dan ayrılmasını sağlar                           |
| `docker service rm`          | Swarm üzerindeki bir servisi siler                               |
| `docker node promote`        | Bir düğümü yöneticilik rolüne yükseltir                          |
| `docker node demote`         | Bir yöneticiyi normal düğüm rolüne indirger                      |
| `docker stack deploy`        | Birden fazla servisi içeren bir yığını dağıtır                   |
| `docker stack ls`            | Dağıtılmış yığınları listeler                                    |
| `docker stack rm`            | Bir yığını kaldırır                                              |
| `docker service ps <ad>`     | Belirli bir servisin görevlerini listeler                        |
| `docker swarm leave --force` | Makinenin swarm'dan zorla ayrılmasını sağlar                     |
