# Yayına Hazırlanma
^^Bu aşamaya geçmeden önce lütfen [Yükleme Talimatları](/yukleme-talimatlari/) sayfasındaki adımları izleyin.^^

[ForFansubs Back-end Node Server Repo](https://github.com/ForFansubs/node-server) karşıdan sadece API servisi olarak görünebilir, ancak bu servis, client ve admin paketlerini serve etmekten de sorumlu. Bu yüzden yayında sadece bu paketi kullanacağız. Diğer paketler front-end'i build'lememize yarayacak. Güncelleme geldikçe tekrardan build edip, aşağıdaki adımları izlerseniz, servisinizi rahatça güncelleyebilirsiniz.

## Front-end paketlerini build'lemek

### Front-end Client
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

`npm run production` komutuyla servisi yayına hazır bir şekilde çalıştırabilirsiniz.
