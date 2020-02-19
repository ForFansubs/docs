# Yükleme Talimatları
Gereken programları indirdiyseniz, boş bir klasör açın.

## Repoları indirme

`git clone https://github.com/ForFansubs/front-end.git`

`git clone https://github.com/ForFansubs/front-end-admin.git`

`git clone https://github.com/ForFansubs/node-server.git`

## Geliştirme ortamını oluşturma

### Back-end
node-server-master dosyasının içinde bir komut ekranı açın. 

- `npm install` yazın. Bu komut servisi çalıştırabilmeniz için gereken paketleri indirip kuracak.

- **./models** klasöründeki SQL dosyasını SQL sunucunuza import edin. (Dosya içerisinde bütün yetkilerin olduğu Yönetici rolü hazır geliyor. Ancak herhangi bir kullanıcı bulunmamakta. Sistemi kurduktan sonra yeni bir kullanıcı açıp, sonrasında rolünü database üzerinden yonetici olarak ayarlamanız gerekiyor. Şu aşamada servisin herhangi bir setup özelliği bulunmamakta.)

- **.env.example** dosyasını kopyalayıp, dosya ismini **.env** yapın ve içerisindeki boş kısımları doldurun. **(NODE_ENV=development olacak)**

- `npm run server` yazın. Bu komutla beraber servis, geliştirme ortamına uygun bir şekilde açılacaktır (hot-load dahil). http://localhost:5000 yolundan servise ulaşabilirsiniz. Ancak şu an size hata verecektir. Çünkü sunacağı dosyaları compile edip gerekli dosyalara koymadık.

### Front-end Client
front-end-master dosyasının içinde bir komut ekranı açın.

- `npm install` yazın.

- **.env.example** dosyasını kopyalayıp, dosya ismini **.env** yapın ve içerisindeki boş kısımları doldurun.

- **./public** yolu içerisinde index.html dosyası açın. İçerisine 

```html
<!DOCTYPE html>
<html lang="tr">
  <head>
    <meta charset="utf-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1" />
    <title>Site name</title>
  </head>
  <body>
    <noscript>
      <style>
        p {
          color: red;
          font-family: 'Roboto', sans-serif;
          font-weight: bold;
          font-size: 36px;
          width: 100vw;
          height: 90vh;
          display: flex;
          align-items: center;
          justify-content: center;
        }
        a {
          margin-left: 10px;
        }
      </style>
      <p>Bu sayfayı görüntülemek için JavaScript'e ihtiyacınız var. Daha iyi bir browser indirmek için <a href="http://outdatedbrowser.com/en" target="_blank">buraya tıklayın.</a></p>
    </noscript>
    <div id="app-mount"></div>
  </body>
</html>
```

kodunu yapıştırabilirsiniz. Bu kod, oldukça biçilmiş bir koddur. "app-mount" kısmı dışında istediğiniz gibi düzenleyebilirsiniz.

- **./src/static** ve **./public/** yollarına programın header ve yükleme/hata kısımlarında gözükecek tam logoyu koyun. İsimleri **fullLogo.png** ve **fullLogo-dark.png** olacak. --- x 150 boyutlarında bir beyaz bir de siyah arka plan için iki farklı versiyon olmak zorunda. [Örnek](../assets/images/fullLogo-dark.png)

- **./src/static** ve **./public/** yollarına kare logoyu koyun. İsmi **logo.png** olacak. 500 x 500 boyutlarında [Örnek](../assets/images/fullLogo.png)

> NOT: Headerınızda gif türünde hareketli logo da kullanabilirsiniz. Yapmanız gereken **static** klasörüne **fullLogo.gif** ve **fullLogo-dark.gif** eklemek, sonrasında da **.env**'e **REACT_APP_HEADER_LOGO_TYPE** ekleyip değerini **"gif"** yapmak.

`npm start` yazarak geliştirici ortamını açabilirsiniz.

### Front-end Admin
front-end-admin-master dosyasının içinde bir komut ekranı açın.

- `npm install` yazın.

- **.env.example** dosyasını kopyalayıp, dosya ismini **.env** yapın ve içerisindeki boş kısımları doldurun.

- **./public** yolu içerisinde index.html dosyası açın. İçerisine 

```html
<!DOCTYPE html>
<html lang="tr">
  <head>
    <meta charset="utf-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1" />
    <title>Site name</title>
  </head>
  <body>
    <noscript>
      <style>
        p {
          color: red;
          font-family: 'Roboto', sans-serif;
          font-weight: bold;
          font-size: 36px;
          width: 100vw;
          height: 90vh;
          display: flex;
          align-items: center;
          justify-content: center;
        }
        a {
          margin-left: 10px;
        }
      </style>
      <p>Bu sayfayı görüntülemek için JavaScript'e ihtiyacınız var. Daha iyi bir browser indirmek için <a href="http://outdatedbrowser.com/en" target="_blank">buraya tıklayın.</a></p>
    </noscript>
    <div id="app-mount"></div>
  </body>
</html>
```

kodunu yapıştırabilirsiniz. Bu kod, oldukça biçilmiş bir koddur. "app-mount" kısmı dışında istediğiniz gibi düzenleyebilirsiniz.

- **./src/static** ve **./public/** yollarına programın header ve yükleme/hata kısımlarında gözükecek tam logoyu koyun. İsmi **fullLogo.png** olacak. --- x 150 boyutlarında [Örnek](../assets/images/fullLogo-light.png)

- **./src/static** ve **./public/** yollarına kare logoyu koyun. İsmi **logo.png** olacak. 500 x 500 boyutlarında [Örnek](../assets/images/fullLogo.png)

> NOT: Headerınızda gif türünde hareketli logo da kullanabilirsiniz. Yapmanız gereken **static** klasörüne **fullLogo.gif** eklemek, sonrasında da **.env**'e **REACT_APP_HEADER_LOGO_TYPE** ekleyip değerini **"gif"** yapmak.

`npm start` yazarak geliştirici ortamını açabilirsiniz.