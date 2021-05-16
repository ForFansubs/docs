# Özel İzleme ve İndirme Siteleri Tanımlama

`./methods/custom` klasöründe bulacağınız `link-extraction-download.js` ve `link-extraction-watch.js` dosyalarını kullanarak sisteminize özel izleme ve indirme siteleri tanımlayabilirsiniz.

### İzleme sitesi ekleme

Bunun için `link-extraction-watch.js` dosyasını kullanmamız gerekiyor. Bu dosya, link tanımlanamazsa `false` tanımlanabilirse aşağıdaki gibi bir obje döndürür.

!!! note "Örnek obje"
    ```js
    {
        src: ""     // String: Embed linki  
        type: ""    // String: Site ismi, hepsi küçük harfle
    }
    ```

Tanımlayacağınız siteler için else if blokları kullanmanız gerekmektedir.

!!! note "Örnek else if bloğu"
    Sisteme girmek istediğimiz linkin `https://custom1.com/video/vHqsyeQexK` olduğunu varsayalım. Aşağıdaki bloğu dosya içinde tanımlayarak, bu linki sisteme kabul ettirebilirsiniz.
    ```js
    else if (link.match(/custom1\.com/)) {
        const videoId = link.split('/')[4] // Yukardaki linki / işareti gördüğümüz yerde bölüyoruz, ve Array içerisindeki son elemente, yani video ID'sine ulaşıyoruz.
        extract.src = `//custom1.com/embed/${videoId}` // Yukarda eriştiğimiz video id'sinden embed linkini oluşturuyoruz. -- Not: Bu embed linki, her site için farklıdır.
        extract.type = 'custom1' // Sitenin ismini küçük harflerle yazıyoruz ve çıkaracağımız objenin "type" keyine eşitliyoruz.
        return extract // Objemizi döndürüyoruz
    }
    ```

### İndirme Sitesi Tanımlama
Bunun için `link-extraction-download.js` dosyasını kullanmamız gerekiyor. Bu dosya, link tanımlanamazsa `false` tanımlanabilirse aşağıdaki gibi bir obje döndürür.

!!! note "Örnek obje"
    ```js
    {
        link: ""     // String: Dosya linki  
        type: ""     // String: Site ismi, hepsi küçük harfle
    }
    ```
    Sizin sadece `type` objesini tanımlamanız gerekiyor, çünkü `link` değeri dosya başında zaten alınıyor.

Ekleyeceğiniz ilk site için if, diğer siteler için else if blokları kullanmanız gerekiyor.

!!! note "Örnek if ve else if blokları"
    Sisteme girmek istediğimiz linklerin `https://custom1.com/video/vHqsyeQexK` ve `https://custom2.com/video/vHqsyeQexK` olduklarını varsayalım. Aşağıdaki bloğu dosya içinde tanımlayarak, bu linkleri sisteme kabul ettirebilirsiniz.
    ```js
    if (link.match(/custom1\.com/)) {
        extract.type = "custom1"
    }
    else if (link.match(/custom2\.com/)) {
        extract.type = "custom2"
    }
    ```