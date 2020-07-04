# Environment Variables (.env)
Yükleme ve yayın sayfalarında .env'den bahsedip durduk. Bu dosyalar, servisin ve front-end paketlerindeki detayların grubunuza özel olmasını sağlayacak değerleri tutuyor.

!!! note "Back-end .env"
    ```env
    PORT=                           // Servisin çalışacağı port.
    HOST_URL=                       // Servisin çalışacağı url. (https://example.com)
    NODE_ENV=                       // Servisin çalışacağı enviroment.
    SITE_NAME=                      // Sitenin ismi. (Örn: PuzzleSubs)
    SECRET_OR_KEY=                  // Passportjs'in kullanacağı secret key.
    DISCORD_ANIME_WH=               // Discord Anime kanalı Webhook
    DISCORD_EPISODE_WH=             // Discord Bölüm kanalı Webhook
    DISCORD_MANGA_WH=               // Discord Manga kanalı Webhook
    DISCORD_MANGA_EPISODE_WH=       // Discord Manga Bölüm kanalı Webhook
    DISCORD_MENTION_ID=             // Discord Webhook mesajlarında mentionlanacak rolün ID'si
    DB_HOST=                        // MariaDB Host
    DB_USER=                        // MariaDB Kullanıcı ismi
    DB_NAME=                        // MariaDB Database ismi
    DB_PASSWORD=                    // MariaDB Kullanıcı şifre
    DB_CONNECTION_LIMIT=100         // MariaDB bağlantı limit sayısı
    SMTP_USERNAME=                  // SMTP Mail için kullanıcı adı
    SMTP_PASSWORD=                  // SMTP Mail için şifre
    SMTP_HOST=                      // SMTP Mail için host
    SMTP_PORT=                      // SMTP Mail için port
    USE_NEW_SEO_METHOD=             // Yeni SEO yöntemini kullanmak istiyorsanız "true"
    PRERENDER_SERVICE_URL=          // Prerender servisinin URL'si
    REDIS_OPTIONS={}                // RedisJS'in createClient fonksiyonunda aldığı options objesi https://redis.js.org/#-api-rediscreateclient
    REDIS_CACHE_TIMEOUT=            // Redis cache süresi (saniye)
    REVERSE_PROXY=                  // Eğer reverse proxy kullanıyorsanız bu değeri true olarak ayarlamanız gerekiyor (Heroku, Bluemix, AWS ELB, Nginx vs.)
    ```

!!! note "Front-end Client .env"
    ```env
    REACT_APP_SITENAME=""           // Sitenin ismi. (Example)
    REACT_APP_SITEURL=""            // Sitenin isim alanı. (https://example.com)
    REACT_APP_INDEX_TITLE_TEXT=     // Index title'da site isminizden sonra gözükecek text. ("Anime ve Manga Çeviri Grubu" gibi)
    REACT_APP_HEADER_LOGO_TYPE=     // Bu değeri "gif" yaparak headerınızda hareketli logo kullanabilirsiniz.
    REACT_APP_DISQUS_SHORTNAME=""   // Disqus kısa ismini sağlarsanız anime, manga ve bölüm sayfalarında yorum kısmı gösterir.
    REACT_APP_DEV_API_URL=""        // Dev ortamında istekleri yapmak için kullanacağı alan adı. (http://localhost:5000 gibi)
    REACT_APP_GA_USER_ID=""         // Google Analytics kullanıcı id'niz.
    REACT_APP_SSS_PAGE=""           // SSS sayfası göstermek istiyorsanız, bu seçeneği `true` olarak ayarlayabilirsiniz. UNUTMAYIN! Sayfanın boş gözükmemesi için `sss_page_text.js` dosyasını doldurmanız gerekiyor.

    REACT_APP_META_DESCRIPTION=     // Sitenin description metasında kullanılacak text.
    REACT_APP_META_AUTHOR=          // Sitenin author metasında kullanılacak text.
    REACT_APP_META_KEYWORDS=        // Sitenin keywords metasında kullanılacak text. (anime, manga, türkçe izle vb.)
    ```

!!! note "Front-end Admin .env"
    ```env
    REACT_APP_SITENAME=             // Sitenin ismi. (Example)
    REACT_APP_SITEURL=              // Sitenin isim alanı. (https://example.com)
    REACT_APP_DEV_API_URL=          // Dev ortamında istekleri yapmak için kullanacağı alan adı. (http://localhost:5000 gibi)
    REACT_APP_HEADER_LOGO_TYPE=     // Bu değeri "gif" yaparak headerınızda hareketli logo kullanabilirsiniz.
    ``` 
