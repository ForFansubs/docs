# Temayı Düzenleme

`./src/config/theming` yolunda `./dark` ve `./light` klasörleri vardır. Bu klasörler içerisinde `index.js` ve `extra.js` dosyaları bulunuyor. İşte bu `extra.js` dosyalarını düzenleyerek, temayı kişiselleştirebilirsiniz.

!!! note "Not"
    İki klasördeki formatta aynı olacağından sadece bir örnek vereceğim. Aynı şeyleri koyu temaya uygun renklerle yaparsanız, istediğiniz sonuçlara ulaşabilirsiniz.

Uygulama, temasını Material UI paketinin sağladığı `theme` objesinden alıyor. Bu yüzden düzenleme yaparken, Material UI'ın `theme` objesine uygun düzenleme yapmamız gerekiyor. Varsayılan `theme` objesine [buradan](https://material-ui.com/customization/default-theme/) ya da uygulamada varolan objeye tarayıcınızdaki Developer Tools konsoluna `theme` yazarak ulaşabilirsiniz.

!!! note "`extra.js` Örnek"
    ```js
        const theme = {
            palette: {
                primary: {
                    main: "#90caf9"
                }
            }
        }

        export default theme
    ```

Yukardaki örnek, ana sayfada öne çıkarılan animeler kısmındaki tür kutularının rengi dahil, butonların renkleri ve sayfalardaki bazı elementlerin rengini değiştirir.

![Tema Örnek 1](../assets/images/TemaOrnek1.png)

Daha ayrıntılı örnekler için `./src/config/theming/index.js`, `./src/config/theming/dark/index.js` ve `./src/config/theming/light/index.js` dosyalarına bakabilirsiniz.
