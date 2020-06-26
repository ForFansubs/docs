# Nasıl Güncellerim

!!! danger "BU SAYFADAKİ ADIMLARI UYGULAMADAN ÖNCE"
    Lütfen bütün dosyalarınızın ve veritabanınızın yedeğini alın. Hiçbir zaman canlıdaki bir veritabanında düzenleme yapılmaması gerektiğini unutmayın.

Aslında aşağıdaki adımları izlemeden, sanki ilk kez kuruyormuşsunuz gibi normal adımları takip ederek sıfırdan kurulum yaparsanız, çok daha sağlıklı bir şekilde kurulumu tamamlayabilirsiniz. Çünkü dosya düzenleri, yeni paket güncellemeleri derken, sorun çıkarabilecek çok şey var. Yine de uğraşmak istemiyorum diyorsanız, aşağıdaki adımları izleyebilirsiniz. Herhangi bir sorunda ilgili paketin github sayfasında yeni bir issue oluşturmayı unutmayın.

## Kurulum aşamaları

1. Öncelikle veritabanı üzerindeki değişiklikleri halletmemiz gerekiyor.
    1. Veritabanınızın yedeğini alın.
    2. Aşağıdaki query komularını, veritabanı sunucunuza yollayın.
```mysql
USE database_name;
ALTER TABLE `anime`
	ADD COLUMN `series_status` CHAR(50) NOT NULL DEFAULT 'Tamamlandı' AFTER `pv`,
	ADD COLUMN `trans_status` CHAR(50) NOT NULL DEFAULT 'Tamamlandı' AFTER `series_status`;
ALTER TABLE `manga`
	ADD COLUMN `series_status` CHAR(50) NOT NULL DEFAULT 'Tamamlandı' AFTER `synopsis`,
	ADD COLUMN `trans_status` CHAR(50) NOT NULL DEFAULT 'Tamamlandı' AFTER `series_status`;
ALTER TABLE `episode` CHANGE COLUMN `seen_download_page` can_user_download tinyint(4);
ALTER TABLE `manga` CHANGE COLUMN `mos_link` reader_link char(255);
ALTER TABLE `user`
	CHANGE COLUMN `activated` `activated` INT(11) NOT NULL DEFAULT '0' AFTER `created_time`;
ALTER TABLE `download_link`
	DROP COLUMN `resolution`;
ALTER TABLE `manga`
	DROP COLUMN `header`;
CREATE TABLE IF NOT EXISTS `manga_episode` (
  `id` int(11) NOT NULL AUTO_INCREMENT,
  `manga_id` int(11) NOT NULL,
  `episode_number` varchar(50) NOT NULL,
  `episode_name` varchar(255) DEFAULT NULL,
  `credits` char(255) DEFAULT NULL,
  `pages` longtext NOT NULL,
  `created_by` int(11) NOT NULL,
  `created_time` datetime DEFAULT current_timestamp(),
  PRIMARY KEY (`id`),
  UNIQUE KEY `id` (`id`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8;
CREATE TABLE IF NOT EXISTS `motd` (
  `id` int(11) NOT NULL AUTO_INCREMENT,
  `is_active` tinyint(4) NOT NULL DEFAULT 1,
  `can_user_dismiss` tinyint(4) DEFAULT 1,
  `title` text DEFAULT NULL,
  `subtitle` text NOT NULL,
  `content_type` char(50) DEFAULT NULL,
  `content_id` int(11) DEFAULT NULL,
  `created_by` int(11) NOT NULL,
  `created_time` datetime NOT NULL DEFAULT current_timestamp(),
  PRIMARY KEY (`id`),
  KEY `id` (`id`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8;
ALTER TABLE `anime`
	CHANGE COLUMN `created_by` `created_by` INT(11) NOT NULL AFTER `created_time`;
ALTER TABLE `manga`
	CHANGE COLUMN `created_by` `created_by` INT(11) NOT NULL AFTER `download_link`;
ALTER TABLE `episode`
	CHANGE COLUMN `created_by` `created_by` INT(11) NOT NULL AFTER `created_time`;
ALTER TABLE `download_link`
	CHANGE COLUMN `created_by` `created_by` INT(11) NOT NULL AFTER `created_time`;
ALTER TABLE `watch_link`
	CHANGE COLUMN `created_by` `created_by` INT(11) NOT NULL AFTER `created_time`;
ALTER TABLE `manga`
	CHANGE COLUMN `reader_link` `reader_link` CHAR(255) NULL DEFAULT NULL COLLATE 'utf8_general_ci' AFTER `mal_link`,
	CHANGE COLUMN `download_link` `download_link` CHAR(255) NULL DEFAULT NULL COLLATE 'utf8_general_ci' AFTER `reader_link`,
	CHANGE COLUMN `created_time` `created_time` DATETIME NOT NULL DEFAULT current_timestamp() AFTER `release_date`;
```

2. Artık `front-end` paketine eklememiz gereken 2 resim daha var.
    1. [CoverPlaceholder.png](../assets/images/CoverPlaceholder.png) ve [HeaderPlaceholder.png](../assets/images/HeaderPlaceholder.png). Örneklerine dosya isiminin üstüne tıklayarak ulaşabilirsiniz. Hazırlayacağınız bu iki dosyayı `./src/static` yoluna koymanız gerekiyor. `CoverPlaceholder` dosyası, anime veya manga cover_art dosyaları sunucunuzda veya database'de ekli `cover_art` linkinde 404 alırsa, 3. bir seçenek olarak gösteriliyor. `HeaderPlaceholder` dosyası ise, sunucunuzda header resmi bulunmayan animelere toplu link eklerseniz, ana sayfada toplu link kısmında gösterilirken kullanılıyor.
3. Ayrıca `front-end` paketindeki bazı özellikleri, artık modüler olarak değiştirebiliyorsunuz. Gelecek dönemde bazılarını database'e taşımayı düşünüyorum, ancak şimdilik her güncelleme geldiğinde tekrardan hazırlamanıza sebep olmayacak bir dosya düzeni var.
    1. `./src/config==` yolundaki `drawer_items.js`, `footer_items.js`, `sss_page_text.js` ve `recruitment_panels.js` dosyalarını, her dosyada bulunan açıklamalara göre değiştirebilirsiniz. {==UNUTMAYIN! `recruitment_panels.js` dosyasını boş bıraksanız bile, sidebar'da Ekip Alımları linkini göstermeye devam edecektir. Bu yüzden boş bırakmamanız tavsiye edilir.==}
4. `node-server` ve `front-end` paketlerinin `.env.example` dosyalarında düzenlemeler yapıldı. Bu değerleri `.env` dosyalarınıza eklemeniz gerekiyor.
    1. `node-server` paketinde aşağıdaki değerler değiştirildi.
```
CF_ZONEID kaldırıldı.
CF_EMAIL  kaldırıldı.
CF_APIKEY kaldırıldı.

REVERSE_PROXY            seçeneği eklendi. // Bu seçeneği eğer reverse proxy kullanıyorsanız `true` olarak ayarlamanız gerekiyor. (Heroku, Bluemix, AWS ELB, Nginx vs.)
DISCORD_MANGA_EPISODE_WH seçeneği eklendi. // Diğer Discord_xx_WH değerleriyle aynı özelliğe sahiptir. Yeni manga bölümü eklendiğinde Discord'a bildirim yollamak için kullanılır.
```

    2. `front-end` paketinde aşağıdaki değerler değiştirildi.
```
REACT_APP_FACEBOOK_LINK kaldırıldı.
REACT_APP_DISCORD_LINK  kaldırıldı.
REACT_APP_SSS_PAGE_TEXT kaldırıldı.

REACT_APP_SSS_PAGE seçeneği eklendi. // SSS sayfası göstermek istiyorsanız, bu seçeneği `true` olarak ayarlayabilirsiniz. UNUTMAYIN! Sayfanın boş gözükmemesi için `sss_page_text.js` dosyasını doldurmanız gerekiyor.
```
5. 3 projedeki paketlerin çoğu güncellendi. Bu yüzden `node-server` servisini çalıştırmadan önce `node_modules` dosyasını silip, `npm install` yapmanız ya da `front-end` veya `front-end-admin` paketlerini buildlemeden önce `node_modules` dosyalarını silip, `yarn install` yapmanız önerilir, yoksa hatalarla karşılaşabilirsiniz.