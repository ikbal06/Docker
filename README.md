# Docker
Uygulama geliştirmek, dağıtmak ve çalıştırmak için kullanılan açık bir platformdur.
Docker Engine: 

-Docker Daemon: objeleri yaratma ve yönetme(linuxe kurar containerle çalıştırır)
-Docker Rest Api: uygulamalar api ile konuşur ve ne yapması gerektiğini söyler(dış dünyayla görüşme)
-Docker CLI: api kullanıcısı, komut satırı arayüzü 
Image: bir uygulamanın çalışması için gerekli tüm kütüphanlerin ve ögelerin paketlenmiş haline denir. İçinde çekirdek(kernel) yok.Bir şablondur.
Container: Imagenin çalışır hali.Şablondan oluşturulan bir kopyadır. İşletim sistemi yoktur. Uygulama sanallaştırılır. Sanal makineden daha hızlıdır. Paketleyip taşıma kolaydır.
Sanal makine: atıl kapasite(boş) yok. Tam bir işletim sistmei barındırır. Fiziksel makine sanallaştırılır.
