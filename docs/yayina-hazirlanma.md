# Yayına Hazırlanma

[ForFansubs NodeApp - Back-End](https://github.com/ayberktandogan/ForFansubs-NodeApp---Back-End) karşıdan sadece API servisi olarak görünebilir, ancak bu servis, client ve admin paketlerini serve etmekten de sorumlu. Bu yüzden yayında sadece bu paketi kullanacağız. Diğer paketler front-end'i build'lememize yarayacak. Güncelleme geldikçe tekrardan build edip, aşağıdaki adımları izlerseniz, servisinizi rahatça güncelleyebilirsiniz.

## Front-end paketlerini build'lemek

### Front-end Client
ForFansubs-ReactApp---Front-end-master dosyasının içinde bir komut ekranı açın.

- `npm run build` yazın. Bu komutla beraber **./** altında **./build** klasörünün oluşturulduğunu göreceksiniz.

### Front-end Admin
ForFansubs-ReactApp-Admin---Front-end-master dosyasının içinde bir komut ekranı açın.

- `npm run build` yazın. Bu komutla beraber **./** altında **./build** klasörünün oluşturulduğunu göreceksiniz.

## Back-end'i yayına hazırlamak
- ForFansubs-NodeApp---Back-End-master dosyasının içine **./admin** ve **./client** klasörlerini oluşturun.

- **ForFansubs-ReactApp---Front-end-master/build** klasörünün içindeki tüm dosyaları kesip, **ForFansubs-NodeApp---Back-End-master/client** dosyasının içerisine yapıştırın.

- **ForFansubs-ReactApp-Admin---Front-end-master/build** klasörünün içindeki tüm dosyaları kesip, **ForFansubs-NodeApp---Back-End-master/admin** dosyasının içerisine yapıştırın.

- **.env.example** dosyasını kopyalayıp, dosya ismini **.env** yapın ve içerisindeki boş kısımları doldurun. **(NODE_ENV=production olacak)**

`npm run production` komutuyla servisi yayına hazır bir şekilde çalıştırabilirsiniz.
