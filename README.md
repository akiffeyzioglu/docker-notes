## Docker Notlarım
Bu repository [A'dan Z'ye Docker](https://www.udemy.com/course/adan-zye-docker "A'dan Z'ye Docker") eğitimini izlerken aldığım notları içermektedir. 

## Docker Nedir?

[Docker](https://tr.wikipedia.org/wiki/Docker "Docker"), "konteynerleştirme" olarak da bilinen işletim sistemi seviyesinde sanallaştırma sağlayan bir bilgisayar programıdır. İlk sürümü 2013'te yayınlanmıştır. Docker, "konteyner" adı verilen yazılım paketlerini çalıştırmak için kullanılmaktadır. 

* Image sadece okunabilir bir ana şablondur, container bu şablonundan oluşturulmuş çalışan bir kopyadır.

* Bir uygulamayı container image olarak paketleyerek üzerinde docker engine olan tüm makinelerde aynı şekilde çalıştırılabilir. 

* Docker CLI, otomatik gelen engine yönetmek için gelen arayüzdür. Daemon ise container oluşturup çalıştıran ana uygulamadır. 

## Container Temelleri
* Her container imajında, o imajdan bir container oluşturduğumuz zaman varsayılan olarak çalışması için ayarlanmış bir uygulama vardır. Bu uygulama çalıştığı sürece container ayakta kalır. Uygulama çalışmayı bıraktığında container da kapatılır.

* Docker Hub, varsayılan imaj çekme deposudur. 

* Docker imajında birden fazla uygulama olabilir.

* Docker, container başlatıldığı zaman otomatik çalışması için tek bir uygulamanın çalışmasına izin verir.

* Container başlatılırken istediğimiz uygulamayı otomatik çalışması için ayarlayabiliriz.

* Aynı imaj dosyası ile farklı containerlar oluşturulabilir. 

## Docker Katmanlı Dosya Sistemi Yapısı

* Docker, 3 katmandan oluşmaktadır. Bu dosya sistemine [Union File System](https://en.wikipedia.org/wiki/UnionFS "Union File System") denir. İlk katmanda işletim sistemin çalışması için gerekli dosyalar bulunur. İkinci katmanda uygulama bulunur. 3. katmanda ise terminal bağlantısı bulunur.

* Bu katmanlar sadece okunabilir katmanlardır. (Read Only - R/O)

* Container oluşturulduğu zaman imaj dosyasının yeni bir kopyasını oluşturmaz. Sistemde aynı imajı farklı containerlar kullanabilir. Yerden tasarruf sağlanıyor ve imaj bir defa ayağa kaldırıldıktan sonra ikinci defa daha hızlı çalışıyor. 

* Tüm katmanlar ayrı ayrı saklanmasına rağmen hepsini bir arada görmemizi Union File System sağlıyor. 

## Docker Volumeler

* [Volumeler](https://docs.docker.com/storage/volumes/ "Volume"), container dışı veri saklamak için kullanılır. 

## Docker Komutları 

`docker version:` Bu komut ile docker sürümünüzü öğrenebilirsiniz. 

`docker info:` Sisteminizde bulunan containerları, ve diğer sistem bilgilerinizi görmenizi sağlar. 

`docker container run hello-world:` hello-world adında container çalıştırır. 

`docker ps:` Çalışan containerları listeler.

`docker ps -a:` Sistem bulunan tüm containerları listeler. 

`docker container ls -a:` "docker ps -a" ile aynı işlevi görür.

`docker container ls -aq:` Sistemde bulunan tüm containerların ID'sini listeler.

`docker container start hello-world:` hello-world containerı başlatır.

`docker container stop hello-world:` hello-world containerını durdurur.

`docker container logs hello-world:` hello-world containerının loglarını gösterir.

`docker image rm "image-name":` Image siler.

`docker container rm "container name or id":` İsmi ya da ID'i verilen containerı siler. 

`docker container prune:` Çalışmayan tüm containerları siler. 

`docker image prune -a:` Çalışmayan tüm imageleri siler.

`docker volume create firstvolume:` firstvolume adında volume oluşturur. 

`docker volume inspect firstvolume:` firstvolume ayrıntılarını verir.

`docker volume ls:` Sistemde bulunan volumeleri listeler.

`docker container run --rm -it hello-world sh:` Containerı çalıştırır. "--rm" container oluşturulduktan sonra sil demektir. "-it" "--interactive" ve "--tty" birleşimidir. Containera interaktif bağlantı yapar. "sh" ile de uzak makinedeki containera terminal bağlantısı ekler. "--rm" sadece container interaktif çalışırken olur. "-d" (detach) ile arka planda çalışsın diyemiyoruz.

`docker history "image-name":` Image'in geçmişini gösterir. 

`docker network ls:` Docker Network objelerini listeler. 

`docker network create "name":` Varsayılan network driverı ile network oluşturur. 

`docker exec -it "container_id" sh:` Uzaktaki containera bir shell bağlantısı ile bağlanmamızı sağlar. 

`docker container run -p 8080:80 "image-name":` Çalıştıracağımız containera port numarası vererek çalıştırabiliriz. 8080 hostun portunu, 80 ise containerın portunu belirtir. 