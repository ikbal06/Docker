# Docker
Uygulama geliştirmek, dağıtmak ve çalıştırmak için kullanılan açık bir platformdur.
Docker Engine: uygulamaları oluşturmak 

-Docker Daemon: objeleri(image) yaratma ve yönetme(linuxe kurar containerle çalıştırır)

-Docker Rest Api: uygulamalar api ile konuşur ve ne yapması gerektiğini söyler(dış dünyayla görüşme)

-Docker CLI: api kullanıcısı, komut satırı arayüzü 

Image: bir uygulamanın çalışması için gerekli tüm kütüphanlerin ve ögelerin paketlenmiş haline denir. İçinde çekirdek(kernel) yok.Bir şablondur.

Container: Imagenin çalışır hali. Şablondan oluşturulan bir kopyadır. İşletim sistemi yoktur. Uygulama sanallaştırılır. Sanal makineden daha hızlıdır. Paketleyip taşıma kolaydır.[bildiğimiz konteynerdan geliyor adı]

Sanal makine: atıl kapasite(boş) yok. Tam bir işletim sistemi barındırır. Fiziksel makine sanallaştırılır.

------CONTAINER101-----------

--help diyerek unuttuğun br komutu nasıl çalıştırabileceğini hatırlayabilirsin
mesela image neydi unuttun docker --help diyerek ya da imageninin altında olan rm(silme komutu) ne olduğunu unuttun docker image  rm -- help diyerek hatırlayabilirsin.

docker container run diyerek önce bir container yaratırsın sonra da o containeri başlatırsın (run=create+start)

Shell, bir kullanıcı ile bir işletim sistemi çekirdeği arasında bir arayüz sağlayan bir programdır.

docker container ls ile oluşturulmuş containerler gözükür -a yaparak sadece çalışan ve durdurulmuşları da görebiliriz.

Her image varsayılan olması için bir uygulama seçer(içinde birden fazla uygulama olabilir ve sadece bir tane uygulama seçebilir) o uygulama çalışırken(bir tane uygulama seçtim -otomotik çalışması için bir tane seçmek zorundayım- ama birden fazla uygulama kullanabilirim) container çalışır uygulama kapandığında container de kapanır.

Varsayılan uygulama yerine başka bir uygulama ile de containeri başlatabilirim.

docker container ls diyince buna random bir isim verdi ama ben docker container run --name X ozgurozturknet/adanzyedocker java app1 diyince artık ismi X oldu

docker container run -d -p 80:80  [buradaki -d arka planda çalıştırıyor] böylece bana hemen bir id verdi
(-d ile arka planda çalışmayı sağlıyor
-p ile istediğim port ta çalışmamı sağlıyor : soldaki docker ın çalışacağı sistem portu sağdaki sağdaki imagenin(uygulamanın) portu)

docker ps (-a)= docker container ls (-a)

kodu silmek için-- docker container rm diyip id den birkaç değer yazıyoruz birden fazla ise bir boşluk koyup diğerini yazıyoruz bu silme işlemi duran kodlar içindir çalışan kodları silemeyiz.

Önce çalışan kodları durdurmak gerekir docker container stop id sonra da rm ile silebilirsin ya da (burası daha kullanışlı) docker container rm -f id diyip de çalışan kodu önce durdurmuş sonra da silmiş oluruz.

sh ile shell e bağlanılıyor

(--interactive)+(--tty)= (--it) => komutlarımı bu container içinde çalıştır ve bunu sağlamak adına sözde bir terminal bağlantısı kurar.

çalışan bir komuta docker container exec(uygula) komutu ile bağlanılır.
docker container exec -it websunucu sh (web sunucu isimli container üzerinde uygula neyi uygula sh komutunu)
bu adımdan sonra ls -l diyerek içindeki dosyaları görebilirim. 

cd /usr/local/apache2/htdocs diyip içine girdim -ps yaparak içindeki uygulamaları görebilirim. exit deyip içinde çıkabilirim ve hala containerim çalışır durumda

kill 1 diyerek ilk uyuglamayı durdurdum containerin ilk uygulaması durduğundan container de durdu.

containera bir şey eklediğim zaman o imageye eklenmez bundan dolayı container durduğunda o eklediğim de durur.

docker container prune sistmedeki durdurulmuş tüm uygulamaları siler(prune: kesmek).

docker image prune -a (tüm imageleri siler).

docker image pull apline (dockerhub üzerindeki apline image nı sisteme çeker)

Özetleyecek olursak;

-Containerlar tek bir uygulamayı çalıştırmak için oluşturulurlar.

-Bu tek bir uygulamayı çalıştırmak için tüm gereksinimlerin önceden hazırladığı imageden yaratılır.

-Container içinde çalışan ana uygulama durduğunda container da durdurulur. Sistemin çalşmaya devam etmesini sağlamak için sistem aynı imageden aynı ayarda yeni bir container yaratabilir.

-Container içindeki uygulamada bir sıkıntı oluşursa container durdurulup yerne yeni bir container yaratrılır. Eğer sıkıntı ayarlarla ilgiliyse image yaratırken çözülür ve yeni bir image ile yeni bir container yaratılır.

Containerler sıklıkla silinip sürekli yenisi oluşturulduğundan(tek kullanımlıktır diyebilirim) önemli verileri orada saklamamalıyım. Bu container dışı veri saklama işine ise volume denir(volume hacim demek ya depo gibi düşünülebilir).

Container ı silsem de oluşturduğum volume silinmez

Bir volume ü biden fazla containera bağlayabilirim.

Eğer bir volume mount edildiği(bağlandığı) klasör yoksa bu klasör yaratılır ve volumeün içinde hangi dosyalar varsa klasörde o dosyalar gözükür.

Eğer ki bir volume imaj içerisinde bulunan bir klasöre mount edilirse:

-Klasör boşsa; olan dosyalar klasörde gözükür

-Klasörde dosya varsa volume boşsa; klasördeki dosyalar volume kopyalanır

-Klasörde dosya var ya da yok fakat volume de dosyalar varsa; klasörün içinde volumede olan dosyayı görürsün.

En sonunda sen o klasöre ne yazarsan yaz o volume yazılır ve container silindiği zaman silinmez.

---------------------CONTAINER102---------------------------

Docker Network Driver

Konteynerların birbileri ve dışarıyla iletişimi docker network objeleri ile sağlanır. Bu objeler de driverlarla sağlanır.

Bridge: varsayılan driver (ping atılabilir)

Host: bazı ihtiyaç hallerinde kullanılır(herhangi bir izolasyon olmadan çalışmaya ihtiyaç duyulduğunda)(üstünde çalıştığı makineye yapışması arada bir şey olmaması)
üzerine bağlı olduğu sistemin altyapısını kullanır

Macvlan: konteynerlara direkt bir mac adresi tanınması gerektiğinde

None: konteynerin hiçbir ağ bağlantısı olmasını istemiyorsak

Overlay: ayrı hostların aynı ağda çalışıyormuş gibi çalışması istendiğinde

docker network ls networkleri sıraladı 

docker network inspect bridge (özelliklerini sıraladı)
inspect i daha detaylı bilgi istediğim zaman kullanabilirim. Mesela image leri sıralarım içinden birini inspectle çalıştırısam seçtiğim hakkında daha detay öğrenebilirm [docker image inspect X]

ctrl pq : konteyner ile bağlantıyı kestik ama kapatmadık

bir bilgisayarın başka bilgisayar arasındaki bağlantı durumunu kontrol etme işlemine ping atmak denir.

docker container run -it --name deneme1 --net host ozgurozturknet/adanzyedocker sh 
[öncelikle bunu playwithdocer sayfasında yapabilirim kendi bilgisayarımda linux işlemcisi sanal olduğu için
(içeriğe gelecek olursak deneme1 adında konteyner oluşturdum sonra host network driverına tarafından oluşturuluş network objesine bağlandım)]

ifconfig ile ağ ayarlarını görebilirim

docker container run -d --publish 8080:80 ozgurozturknet/adanzyedocker
(bu host üzerinde konteyner yarat ve hostun 8080 portuna gelen bütün istekleri de yarattığım konteyner 80 portunun üstüne gönder)

-p host_port:container_port

yukarıdaki konteyner açıldığı zaman hostun 8080 portuna istek gönderdiğim zaman alınacak ve konteynerin içindeki 80 portuna gönderilecek ve cevap oradan gelecek 

Konteynerlar arası network izolasyonu sağlamak istersek ayrı bridge network yaratarak yapabiliriz.

Varsayılan dışında ip aralıkları tanımlanabilir

Aynı networke bağlı konteynerlar birbirlerinin isimlerini çözebilirler

Kullanıcı tanımlı konteynerın bağlı olduğu bridge networkle bağlantısını kesemezsin

Kullanıcının yarattığı bridge networkleri bağlarsın da bağlantısını kesersin de

-dit (-d + -it) interaktif bağlantı kur, arka planda yap

attach çalışan konteynerı etkileşimşi hale getirmek için kullanılır bunu yazınca 
/usr/src/myapp tarzı bir şey gelir onun içine yazarım

ctrl c ile ping durdurulur

--subnet alt ağ

--ip-range=10.10.10.0/24 >> subnetin dağıtacağı ip adres aralığı

--gateway=10.10.10.10 konteynera bağlanan bridge network


Standart Input-Output-Error: o komutun ya da terminalin bizimle iletişim kurma yolu

stdin(0): uygulamanın giriş akışıdır(klavyeden yazdıklarım)

stdout(1): uygulamanın genel çıktısıdır(uygulama bir cevap oluşturursa bunu ekranda gösterir)

stderr(2): hata mesajı için

docker logs --details con1 (con1 hakkında daha detaylı bilgi için)

docker logs -t con1 (ile tarihli)

docker logs --until 2022-04-19T10:54:50.942949800Z con1 (bana bu tarihe kadar olan logları göster demek)

until yerine since dersem de o tarihten sonraki logları bana gösterir

docker logs --tail 3 con1 (oluşan son 3 logu gösterir)

docker logs -f con1 (konteyner üzerinde oluşan canlı logları görmek için (-f =follow)) ctrl c ile de o ekrandan çıkabilirm

docker container run --log-driver splunk ngnix (splunk logunu çalıştırmış oldum nginx ten konteyner oluştumuş oldum (şu an splunk driverı ayarlı olmadığından hata verdi ayarlı olsaydı bu konteyner merkezi değişmiş olacaktı))

docker top con1 (con1 in proseslerini verir)

docker stats (docker üzerinde çalışan tüm konteynerları(ve durumlarını) verir ve yeniler)

docker stats X (x konteynerının durumunu verir)

docker container run -d --memory=100m --memory-swap=200m ozgurozturknet/adanzyedocker (ben sistemme 100mb lık yer açtım eğer ihtiyaç varsa 100 daha kullanabilirsin)


























