# Yayına Hazırlanma
^^Bu aşamaya geçmeden önce lütfen [Yükleme Talimatları](../yukleme-talimatlari/) sayfasındaki adımları izleyin.^^

[ForFansubs Back-end Node Server Repo](https://github.com/ForFansubs/node-server) karşıdan sadece API servisi olarak görünebilir, ancak bu servis, client ve admin paketlerini serve etmekten de sorumlu. Bu yüzden yayında sadece bu paketi kullanacağız. Diğer paketler front-end'i build'lememize yarayacak. Güncelleme geldikçe tekrardan build edip, aşağıdaki adımları izlerseniz, servisinizi rahatça güncelleyebilirsiniz.

## Front-end paketlerini build'lemek

### Front-end Client

Gerekli bütün resimleri ilgili dosyalara attığınızdan, `./src/config` dosyasında bulunan `recruitment_panels.js` dosyanına en azından bir panel eklediğinizden emin olun. Çünkü bu dosya boş olsa bile sidebarda Ekip Alımları sekmesi gözükmeye devam ediyor ve kullanıcı sayfaya girdiğinde boş bir sayfayla karşılaşıyor.
 
front-end-master dosyasının içinde bir komut ekranı açın.

- `npm run build` yazın. Bu komutla beraber {==./==} altında {==./build==} klasörünün oluşturulduğunu göreceksiniz.

### Front-end Admin
front-end-admin-master dosyasının içinde bir komut ekranı açın.

- `npm run build` yazın. Bu komutla beraber {==./==} altında {==./build==} klasörünün oluşturulduğunu göreceksiniz.

## Back-end'i yayına hazırlamak
- node-server-master dosyasının içine {==./admin==} ve {==./client==} klasörlerini oluşturun.

- {==./front-end-master/build==} klasörünün içindeki tüm dosyaları kesip, {==./node-server-master/client==} dosyasının içerisine yapıştırın.

- {==./front-end-admin-master/build==} klasörünün içindeki tüm dosyaları kesip, {==./node-server-master/admin==} dosyasının içerisine yapıştırın.

- {==.env.example==} dosyasını kopyalayıp, dosya ismini {==.env==} yapın ve içerisindeki boş kısımları doldurun. {>>NODE_ENV=production<<}

---

Aşağıdaki seçeneklerden birisini kullanarak, servisinizi yayına çıkarabilirsiniz.

=== "pm2 Kullanarak"
    `pm2` paketi nasıl kullanılır detaylarına girmeyeceğim. Nasıl kurulduğuna [buradaki linkten](https://pm2.keymetrics.io/) ulaşabilirsiniz. Neden kullanacağız derseniz de, pm2'nin normalde scriptler yazarak elde edebileceğimiz şeyleri otomatik bir şekilde yapabildiği için. En basitinden, servis çöktüğü zaman yeniden başlatması, bir dosya değiştiğinde servisi yeniden başlatması vs. Bütün bu özelliklere ve detaylara yukardaki linkten ulaşabilirsiniz.

    node-server dosyanızın içerisinde {==ecosystem.config.js==} adlı bir dosya açın. İçerisinde aşağıdaki örnek gibi bir ayar objesi çıkarmanız gerekiyor. Bu ayarları neye göre değiştireceğinize, nasıl kullanacağınıza [buradaki linkten](https://pm2.keymetrics.io/docs/usage/application-declaration/) ulaşabilirsiniz. Özellikle cluster modunun nasıl kullanılacağını öğrenirseniz servisi çok rahatlatabilirsiniz.
    ```js
    module.exports = {
    apps: [{
        "name": "FFs Node Server",
        "script": "server.js",
        "instances": "max",
        "exec_mode": "cluster"
        }]
    }
    ```
    
    Bu adımı gerçekleştirdikten sonra dosyanız içerisindeki komut ekranında

    `pm2 start`

    yazarsanız, servisiniz pm2 üzerinden çalışmaya başlar.

=== "Normal yolla"
    `npm run production` komutuyla servisi yayına hazır bir şekilde çalıştırabilirsiniz.
