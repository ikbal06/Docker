# Docker
Uygulama geliştirmek, dağıtmak ve çalıştırmak için kullanılan açık bir platformdur.
Docker Engine: 

-Docker Daemon: objeleri yaratma ve yönetme(linuxe kurar containerle çalıştırır)

-Docker Rest Api: uygulamalar api ile konuşur ve ne yapması gerektiğini söyler(dış dünyayla görüşme)

-Docker CLI: api kullanıcısı, komut satırı arayüzü 

Image: bir uygulamanın çalışması için gerekli tüm kütüphanlerin ve ögelerin paketlenmiş haline denir. İçinde çekirdek(kernel) yok.Bir şablondur.

Container: Imagenin çalışır hali. Şablondan oluşturulan bir kopyadır. İşletim sistemi yoktur. Uygulama sanallaştırılır. Sanal makineden daha hızlıdır. Paketleyip taşıma kolaydır.

Sanal makine: atıl kapasite(boş) yok. Tam bir işletim sistmei barındırır. Fiziksel makine sanallaştırılır.

------CONTAINER101-----------

--help diyerek unuttuğun br komutu nasıl çalıştırabileceğini hatırlayabilirsin
mesela image neydi unuttun docker --help diyerek ya da imageninin altında olan rm(silme komutu) ne olduğunu unuttun docker image  rm -- help diyerek hatırlayabilirsin.

docker container run diyerek önce bir container yaratırsın sonra da o containeri başlatırsın (run=create+start)

Shell, bir kullanıcı ile bir işletim sistemi çekirdeği arasında bir arayüz sağlayan bir programdır.

docker container ls ile oluşturulmuş containerler gözükür -a yaparak sadece çalışan ve durdurulmuşları da görebiliriz.

Her image varsayılan olması için bir uygulama seçer(içinde birden fazla uygulama olabilir ve sadece bir tane uygulama seçeiblir) o uygulama çalışırken(bir tane uygulama seçtim-otomotik çalışması için bir tane seçmek zorundayım- ama birden fazla uygulama kullanabilirim) container çalışır uygulama kapandığında container de kapanır.

Varsayılan uygulama yerine başka bir uygulama ile de containeri başlatabilirim.

docker container ls diyince buna random bir isim verdi ama ben dcoker container run --name X ozgurozturknet/adanzyedocker java app1 diyince artık ismi X oldu

docker container run -d -p 80:80  [buradaki -d arka planda çalıştırıyor] böylece bana hemen bir id verdi

docker ps (-a)= docker container ls (-a)

kodu silmek için-- docker container rm diyip id den birkaç değer yazıyoruz birden fazla ise bir boşluk koyup diğerini yazıyoruz bu silme işlemi duran kodlar içindir çalışan kodları silemeyiz.

Önce çalışan kodları durdurmak gerekir docker container stop id sonra da rm ile silebilirsin ya da (burası daha kullanışlı) docker container rm -f id diyip de çalışan kodu önce durdurmuş sonra da silmiş oluruz.

sh ile shell e bağlanılıyor

(--interactive)+(--tty)= (--it) => komutlarımı bu container içinde çalıştır ve bunu sağlamak adına sözde bir terminal bağlantısı kurar.
