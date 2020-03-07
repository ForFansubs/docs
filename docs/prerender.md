# Prerender (SEO)
Yeni SEO yöntemini kullanabilmek için sunucunuz üzerinde Prerender.io servisini hostlamanız gerekiyor.

## Kurulum
!!! important "İndirme linki"
    [Prerender](https://github.com/prerender/prerender) paketini bu linkten direkt olarak indirebilir ya da clonelayabilirsiniz.

Bu aşamadan sonra paket dosyasında `npm install` yaptıktan sonra direkt olarak `node server.js` ile servisi çalıştırabilirsiniz. Servis ayarlarının detaylarına çok girmek istemiyorum, kendi sayfası üzerinden bakabilirsiniz.

Servisi kurup çalıştırdıktan sonra sistemde hangi port üzerinde çalışıyorsa, {==node-server .env==} içerisindeki {==PRERENDER_SERVICE_URL==} değerini ona göre ayarlayıp, node-server'ı başlatmanız gerekiyor.

!!! important "Eklenmesi gereken örnek .env (Son güncelleme: 7 Mart)"
    ```env
    USE_NEW_SEO_METHOD="true"
    PRERENDER_SERVICE_URL="http://localhost:3002"
    REDIS_OPTIONS={}                                // {"port": 1001, "host": 255.255.255.0} gibi
    REDIS_CACHE_TIMEOUT=259200
    ```

!!! note "Neden Memurai?"
    Sistemi yazdığım ve test ettiğim ortam Windows. Redis, Windows'u native olarak desteklemediği için, farklı yöntemlere yönelmem gerekti. Memurai'de Redis tabanlı yazıldığı için, Redis'i kullanan paketlerle uyumlu. Eğer sistemi Windows ortamda barındıracaksınız kullanabilirsiniz.

!!! note "Neden Prerender?"
    React, doğası gereği Google dışındaki arama servisleri ve crawlerlarda doğru renderlanamıyor. Pre-render tam da bu arada devreye giriyor. Bu tip sistemlere "html" tabanlı cevap gönderiyor ve renderın gerektiği gibi yürümesini sağlıyor.

    Neden hostlamamız gerekiyor diye soracak olursanız da, kendi sundukları çözüm paralı. Detaylarına [prerender.io](https://prerender.io) sitesinden bakabilirsiniz.
