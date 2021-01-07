# Docker Notlarım
Bu repository [A'dan Z'ye Docker](https://www.udemy.com/course/adan-zye-docker "A'dan Z'ye Docker") eğitimini izlerken aldığım notları içermektedir. 

## İçerik Tablosu

* [Docker Nedir](#Docker-Nedir)
* [Container Temelleri](#Container-Temelleri)
* [Docker'ın Katmanlı Dosya Sistemi Yapısı](#Docker'ın-Katmanlı-Dosya-Sistemi-Yapısı)
* [Docker Volume'ler](#Docker-Volume'ler)
* [Docker Network Objeleri](#Docker-Network-Objeleri)
* [Docker İmaj İsimlendirme](#Docker-İmaj-İsimlendirme)
* [Dockerfile](#Dockerfile)
* [Multi Stage Build](#Multi-Stage-Build)
* [Docker Save and Load](#Docker-Save-and-Load)
* [Ortam Değişkenleri](#Ortam-Değişkenleri)
* [Docker Komutları](#Docker-Komutları)
  * [Genel](#Genel)
  * [Container](#Container)
  * [Image](#Image)
  * [Volume](#Volume)
  * [Network](#Network)
  * [Logs](#Logs)
  * [Save and Load](#Save-and-Load)
  * [Docker Commit](#Docker-Commit)

# Docker Nedir?

[Docker](https://tr.wikipedia.org/wiki/Docker "Docker"), "konteynerleştirme" olarak da bilinen işletim sistemi seviyesinde sanallaştırma sağlayan bir bilgisayar programıdır. İlk sürümü 2013'te yayınlanmıştır. Docker, "konteyner" adı verilen yazılım paketlerini çalıştırmak için kullanılmaktadır. 

* Image sadece okunabilir bir ana şablondur, container bu şablonundan oluşturulmuş çalışan bir kopyadır.

* Bir uygulamayı container image olarak paketleyerek üzerinde docker engine olan tüm makinelerde aynı şekilde çalıştırılabilir. 

* Docker CLI, otomatik gelen engine yönetmek için gelen arayüzdür. Daemon ise container oluşturup çalıştıran ana uygulamadır. 

# Container Temelleri
* Her container imajında, o imajdan bir container oluşturduğumuz zaman varsayılan olarak çalışması için ayarlanmış bir uygulama vardır. Bu uygulama çalıştığı sürece container ayakta kalır. Uygulama çalışmayı bıraktığında container da kapatılır.

* Docker Hub, varsayılan imaj çekme deposudur. 

* Docker imajında birden fazla uygulama olabilir.

* Docker, container başlatıldığı zaman otomatik çalışması için tek bir uygulamanın çalışmasına izin verir.

* Container başlatılırken istediğimiz uygulamayı otomatik çalışması için ayarlayabiliriz.

* Aynı imaj dosyası ile farklı containerlar oluşturulabilir. 

* Her container limit berlirtilmezse sistem kaynaklarının tamamını kullanabilir. 

# Docker'ın Katmanlı Dosya Sistemi Yapısı

* Docker, 3 katmandan oluşmaktadır. Bu dosya sistemine [Union File System](https://en.wikipedia.org/wiki/UnionFS "Union File System") denir. İlk katmanda işletim sistemin çalışması için gerekli dosyalar bulunur. İkinci katmanda uygulama bulunur. 3. katmanda ise terminal bağlantısı bulunur.

* Bu katmanlar sadece okunabilir katmanlardır. (Read Only - R/O)

* Container oluşturulduğu zaman imaj dosyasının yeni bir kopyasını oluşturmaz. Sistemde aynı imajı farklı containerlar kullanabilir. Yerden tasarruf sağlanıyor ve imaj bir defa ayağa kaldırıldıktan sonra ikinci defa daha hızlı çalışıyor. 

* Tüm katmanlar ayrı ayrı saklanmasına rağmen hepsini bir arada görmemizi Union File System sağlıyor. 

# Docker Volume'ler

* [Volumeler](https://docs.docker.com/storage/volumes/ "Volume"), container dışı veri saklamak için kullanılır. 

# Docker Network Objeleri

* Default gelen 3 network driverı vardır. Bridge, Host ve None.

* Docker'ın default network driverı Bridge'dir.

* Aynı network driverına bağlı containerlar birbirleriyle direkt haberleşebilirler.

* Host networku direkt sistemdeki ağı kullanır. Arada bir izolasyon yoktur.

* none driverı network bağlantısı sağlamaz.

* Default TCP ile çalışır. UDP de çalışabilir.

* Bir container birden fazla networke bağlanabilir.

# Docker İmaj İsimlendirme

* Docker imajlarına verilen isimler depolandığı yeri belirtir.

* Docker'da her objenin eşsiz bir ID'si vardır.

* İmaj isminin ilk kısmı registry URL, ikinci kısmı repository ve üçüncü kısmı ise tagdir.

* Tag yapısı ile birden fazla imajın saklanabilmesi sağlanır.

- Spesifik tag belirtilmezse default latet tagi ile işlem yapılır.

# Dockerfile

* Dockerfile dosyası oluşturulurken "Dockerfile" şeklinde oluşturulmalıdır. Uzantı belirtilmesine gerek yoktur.

* Dockerfile oluştururken komutların sıralaması önemlidir.

* ENV komutu Dockerfile içerisinde yazılmazsa, ortam değişkenleri base imajdan gelir.

* Dockerfile dosyasında birdene fazla FROM komutu olabilir.

`Komutlar:`

* FROM: Oluşturulacak imajın hangi base imajdan oluşturulacağını belirtir. Dockerfile dosyası içerinde olması zorunlu olan tek komuttur.

* RUN: İmaj oluşturulurken Shell'de çalışması gereken bir komut varsa RUN ile yazılır.

* WORKDIR: Dizin değiştirmek için kullanılır. cd komutu ile tek farkı dizin yoksa oluşturulur.

* COPY: İmajın içerisine dosya kopyalar.

* ADD: İmajın içerisine dosya ekler. 

* ARG: İmaj build edilirken argüman almasını sağlar.

* EXPOSE: Bu imajdan oluşturulacak containerların hangi portlar üzerinden yayınlanacağını EXPOSE ile belirtilir.

* CMD: Bu imajdan container oluşturulduğu zaman varsayılan olarak çalıştırılmak istenen komut yazılır.

* HEALTHCHECK: Bu komut ile containerın çalışıp çalışmadığı kontrol edilebilir. 

* ENV: Ortam değişkeni tanımlanmasını sağlar.

* LABEL: Bu komut Dockerfile içerisine metadata ekler. 

`ADD ve COPY Farkı`

* ADD ile COPY aynı işlevleri görür fakat ADD dosya kaynağının URL olmasını da sağlar.

* ADD ile bir .tar dosyası belirtilirse bu arşiv imaja untar yapılarak kopyalanır.

`ENTRYPOINT ve CMD Farkı`

* ENTRYPOINT, CMD gibi imaj oluşturulduktan sonra değiştirilemez.

* Her iki komutta yazılıyorsa CMD komutunda yazılanlar ENTRYPOINT'e parametre olarak eklenir.

# Multi Stage Build

* Bu özellik sayesinde imaj oluşturma aşamaları kademelere bölünebilir.

* Bu sayede ilk kademede oluşturulan imaj içerisindeki dosyaları bir sonraki kademede oluşturacağımız imaja kopyalayabilmemize olanak sağlar. 

# Docker Save and Load

* Bu özellik sayesinde imaj bir tar arşivine dönüştürülebilir. 

* Aynı şekilde tar arşivi de imaja dönüştürülebilir. 

# Ortam Değişkenleri

* Ortam değişkenleri tanımlanırken büyük küçük harflere dikkat edilmelidir. deg1 ile DEG1 aynı şeyler değildir. 

# Docker Komutları 

## Genel

`docker version:` Bu komut ile docker sürümünüzü öğrenebilirsiniz. 

`docker info:` Sisteminizde bulunan containerları, ve diğer sistem bilgilerinizi görmenizi sağlar. 

## Container

`docker ps:` Çalışan containerları listeler.

`docker ps -a:` Sistem bulunan tüm containerları listeler. 

`docker container ls -a:` "docker ps -a" ile aynı işlevi görür.

`docker container ls -aq:` Sistemde bulunan tüm containerların ID'sini listeler.

`docker container run hello-world:` hello-world adında container çalıştırır. 

`docker container start hello-world:` hello-world containerı başlatır.

`docker container stop hello-world:` hello-world containerını durdurur.

`docker container logs hello-world:` hello-world containerının loglarını gösterir.

`docker container run -p 8080:80 "image-name":` Çalıştırılan containera port numarası verilerek çalıştırabilir. 8080 hostun portunu, 80 ise containerın portunu belirtir. 

`docker container run -dit "image-name" sh:` "-dit" komutu -d -it -tty birleşimidir. Containera interaktiflik ve sözde terminal bağlantısını ekleyerek arka planda çalıştırır. 

`docker container run -dit --net "network-name" "image-name" sh:` Oluşturulan network ile container oluşturur. 

`docker exec -it "container_id" sh:` Uzaktaki containera bir shell bağlantısı ile bağlanmamızı sağlar. 

`docker top "container name or id:` Containerda hangi işlemlerin çalıştığını gösterir.

`docker container run --rm -it hello-world sh:` Containerı çalıştırır. "--rm" container oluşturulduktan sonra sil demektir. "-it" "--interactive" ve "--tty" birleşimidir. Containera interaktif bağlantı yapar. "sh" ile de uzak makinedeki containera terminal bağlantısı ekler. "--rm" sadece container interaktif çalışırken olur. "-d" (detach) ile arka planda çalışsın diyemiyoruz.

`docker stats "container name or id":` Çalışan containerın ne kadar kaynak kullandığını gösterir. 

`docker attach "container-name or id":` Arka planda çalıştırılan containera bağlanmak için kullanılır. 

`docker container run -d --memory=100m "image-name":` Oluşturulacak containera 100mb bellek limiti tanımlar. 

`docker container run -d --cpus="1.5" "image-name:` Sistemde bulunan işlemci çekirdeklerinin 1.5 tanesini kullanmasını sağlar. 

`docker container run -d --cpuset-cpus="1,4" "image-name":` Sistemde bulunan işlemcinin 1 ve 4 numaralı işlemcilerini kullanmasını sağlar. 

`docker container run --env deg1=deneme "image-name":` deg1 adında ortam değişkeni tanımlar.

`docker container rm "container name or id":` İsmi ya da ID'i verilen containerı siler. 

`docker container rm -f "container name or id":` İsmi ya da ID'si verilen containerı çalışırken dahi siler. 

`docker container prune:` Çalışmayan tüm containerları siler. 

# Image

`docker image build -t image-name .:` Dockerfile yazılıktan sonra image build işlemini gerçekleştirir. 

`docker image build -t "image-name" -f "dockerfile-name" .:` Farklı bir Dockerfile'dan imaj build eder. 

`docker image rm "image-name":` İmaj siler.

`docker image prune -a:` Çalışmayan tüm imajları siler.

`docker history "image-name":` İmaj'ın geçmişini gösterir. 

# Volume

`docker volume create firstvolume:` firstvolume adında volume oluşturur. 

`docker volume inspect firstvolume:` firstvolume ayrıntılarını verir.

`docker volume ls:` Sistemde bulunan volumeleri listeler.

`docker volume rm "volume-name":` Adı verilen volumeü siler. 

`docker volume prune:` Sistemde bulunan tüm volumeleri siler. 

# Network

`docker network create "name":` Varsayılan network driverı ile network oluşturur. 

`docker network ls:` Docker Network objelerini listeler. 

`docker network connect "network-name" "container name or id":` Adı veya ID'si verilen containerı kullanıcı tarafından oluşturulan networke bağlamayı sağlar. Network bağlama işlemi sadece kullanıcı tarafından oluşturulan networkte yapılabilir. 

`docker network disconnect "network-name" "container name or id":` Adı veya ID'si verilen containerı kullanıcı tarafından oluşturulan network ile bağlantısını keser. 

`docker network rm "network-name:` Network silmeyi sağlar. 

# Logs

`docker logs "container name or id":` Container çalıştıktan sonra logları getirir. 

`docker logs -f "container name or id":` Çalışan containerın anlık loglarını gösterir.

# Save and Load

* `docker save "image-name" -o "image-name.tar":` İmajı tar arşivine dönüştürür.

* `docker load -i "image-name.tar":` tar arşivini imaja çevirir. 

# Docker Commit 

* `docker commit "container-id" "image-name":` Container'daki değişikliklerden yeni bir imaj oluşturur. 