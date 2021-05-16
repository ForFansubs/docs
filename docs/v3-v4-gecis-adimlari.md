# Nasıl Güncellerim

!!! danger "BU SAYFADAKİ ADIMLARI UYGULAMADAN ÖNCE"
    Lütfen bütün dosyalarınızın ve veritabanınızın yedeğini alın. Hiçbir zaman canlıdaki bir veritabanında düzenleme yapılmaması gerektiğini unutmayın.

Aslında aşağıdaki adımları izlemeden, sanki ilk kez kuruyormuşsunuz gibi normal adımları takip ederek sıfırdan kurulum yaparsanız, çok daha sağlıklı bir şekilde kurulumu tamamlayabilirsiniz. Çünkü dosya düzenleri, yeni paket güncellemeleri derken, sorun çıkarabilecek çok şey var. Yine de uğraşmak istemiyorum diyorsanız, aşağıdaki adımları izleyebilirsiniz. Herhangi bir sorunda ilgili paketin github sayfasında yeni bir issue oluşturmayı unutmayın.

## Kurulum aşamaları

1. Öncelikle veritabanı üzerindeki değişiklikleri halletmemiz gerekiyor.
    1. Veritabanınızın yedeğini alın.
    2. Aşağıdaki query komularını, veritabanı sunucunuza yollayın.
```mysql
USE fgl_nodejs_test;
ALTER TABLE `anime`
	CHANGE COLUMN `created_by` `created_by` INT(11) NULL AFTER `created_time`;
ALTER TABLE `manga`
	CHANGE COLUMN `created_by` `created_by` INT(11) NULL AFTER `created_time`;
ALTER TABLE `download_link`
	CHANGE COLUMN `created_by` `created_by` INT(11) NULL AFTER `created_time`;
ALTER TABLE `watch_link`
	CHANGE COLUMN `created_by` `created_by` INT(11) NULL AFTER `created_time`;
ALTER TABLE `episode`
	CHANGE COLUMN `created_by` `created_by` INT(11) NULL AFTER `created_time`;
ALTER TABLE `manga_episode`
	CHANGE COLUMN `created_by` `created_by` INT(11) NULL AFTER `created_time`;
ALTER TABLE `motd`
	CHANGE COLUMN `created_by` `created_by` INT(11) NULL AFTER `created_time`;
ALTER TABLE `pending_user`
	CHANGE COLUMN `user_id` `user_id` INT(11) NOT NULL;
ALTER TABLE `user`
	CHANGE COLUMN `id` `id` INT(11) NOT NULL AUTO_INCREMENT FIRST;
DELETE FROM watch_link WHERE anime_id NOT IN (SELECT id FROM anime);
DELETE FROM watch_link WHERE episode_id NOT IN (SELECT id FROM episode);
DELETE FROM download_link WHERE anime_id NOT IN (SELECT id FROM anime);
DELETE FROM download_link WHERE episode_id NOT IN (SELECT id FROM episode);
ALTER TABLE `watch_link`
	ADD CONSTRAINT `watch_link_anime_id_fk` FOREIGN KEY (`anime_id`) REFERENCES `anime` (`id`) ON UPDATE CASCADE ON DELETE CASCADE;
ALTER TABLE `watch_link`
	ADD CONSTRAINT `watch_link_episode_id_fk` FOREIGN KEY (`episode_id`) REFERENCES `episode` (`id`) ON UPDATE CASCADE ON DELETE CASCADE;
ALTER TABLE `watch_link`
	ADD CONSTRAINT `watch_link_created_by_fk` FOREIGN KEY (`created_by`) REFERENCES `user` (`id`) ON UPDATE CASCADE ON DELETE SET NULL;
ALTER TABLE `download_link`
	ADD CONSTRAINT `download_link_anime_id_fk` FOREIGN KEY (`anime_id`) REFERENCES `anime` (`id`) ON UPDATE CASCADE ON DELETE CASCADE;
ALTER TABLE `download_link`
	ADD CONSTRAINT `download_link_episode_id_fk` FOREIGN KEY (`episode_id`) REFERENCES `episode` (`id`) ON UPDATE CASCADE ON DELETE CASCADE;
ALTER TABLE `download_link`
	ADD CONSTRAINT `download_link_created_by_fk` FOREIGN KEY (`created_by`) REFERENCES `user` (`id`) ON UPDATE CASCADE ON DELETE SET NULL;
ALTER TABLE `episode`
	ADD CONSTRAINT `episode_anime_id_fk` FOREIGN KEY (`anime_id`) REFERENCES `anime` (`id`) ON UPDATE CASCADE ON DELETE CASCADE;
ALTER TABLE `manga_episode`
	ADD CONSTRAINT `manga_episode_manga_id_fk` FOREIGN KEY (`manga_id`) REFERENCES `manga` (`id`) ON UPDATE CASCADE ON DELETE CASCADE;
ALTER TABLE `anime`
	ADD CONSTRAINT `anime_created_by_fk` FOREIGN KEY (`created_by`) REFERENCES `user` (`id`) ON UPDATE CASCADE ON DELETE SET NULL;
ALTER TABLE `manga`
	ADD CONSTRAINT `manga_created_by_fk` FOREIGN KEY (`created_by`) REFERENCES `user` (`id`) ON UPDATE CASCADE ON DELETE SET NULL;
ALTER TABLE `episode`
	ADD CONSTRAINT `episode_created_by_fk` FOREIGN KEY (`created_by`) REFERENCES `user` (`id`) ON UPDATE CASCADE ON DELETE SET NULL;
ALTER TABLE `manga_episode`
	ADD CONSTRAINT `manga_episode_created_by_fk` FOREIGN KEY (`created_by`) REFERENCES `user` (`id`) ON UPDATE CASCADE ON DELETE SET NULL;
UPDATE anime
	SET series_status = "finished_airing"
	WHERE series_status = "Tamamlandı";
UPDATE anime
	SET trans_status = "finished_airing"
	WHERE trans_status = "Tamamlandı";
UPDATE anime
	SET series_status = "not_aired_yet"
	WHERE series_status = "Daha yayınlanmadı";
UPDATE anime
	SET trans_status = "not_aired_yet"
	WHERE trans_status = "Daha yayınlanmadı";
UPDATE anime
	SET series_status = "currently_airing"
	WHERE series_status = "Devam ediyor";
UPDATE anime
	SET trans_status = "currently_airing"
	WHERE trans_status = "Devam ediyor";
UPDATE anime
	SET series_status = "postponed"
	WHERE series_status = "Ertelendi";
UPDATE anime
	SET trans_status = "postponed"
	WHERE trans_status = "Ertelendi";
UPDATE anime
	SET series_status = "canceled"
	WHERE series_status = "İptal edildi";
UPDATE anime
	SET trans_status = "canceled"
	WHERE trans_status = "İptal edildi";
UPDATE manga
	SET series_status = "finished_airing"
	WHERE series_status = "Tamamlandı";
UPDATE manga
	SET trans_status = "finished_airing"
	WHERE trans_status = "Tamamlandı";
UPDATE manga
	SET series_status = "not_aired_yet"
	WHERE series_status = "Daha yayınlanmadı";
UPDATE manga
	SET trans_status = "not_aired_yet"
	WHERE trans_status = "Daha yayınlanmadı";
UPDATE manga
	SET series_status = "currently_airing"
	WHERE series_status = "Devam ediyor";
UPDATE manga
	SET trans_status = "currently_airing"
	WHERE trans_status = "Devam ediyor";
UPDATE manga
	SET series_status = "postponed"
	WHERE series_status = "Ertelendi";
UPDATE manga
	SET trans_status = "postponed"
	WHERE trans_status = "Ertelendi";
UPDATE manga
	SET series_status = "canceled"
	WHERE series_status = "İptal edildi";
UPDATE manga
	SET trans_status = "canceled"
	WHERE trans_status = "İptal edildi";
ALTER TABLE `manga`
	ADD COLUMN `is_featured` TINYINT(1) NOT NULL DEFAULT 0 AFTER `synopsis`;
```

2. Artık `node-server` paketine eklememiz gereken 1 resim var.
    1. `front-end` paketinde kullanmış olduğunuz `logo.png` görselini `node-server` paketi içerisinde `./images/static` yoluna koymanız gerekiyor. Klasör açılmamışsa, açabilirsiniz.
3. `node-server` paketi içerisinde `./images/metadata` klasörü ve içerisinde `./images/metadata/anime` ve `./images/metadata/manga` yolları bulunmuyorsa oluşturun. Sistemin zaten açmaya çalıştığınızda uyarı vermesi gerekiyor ama, olsun.
4. `node-server`, `front-end` ve `front-end-admin` paketlerinin `.env.example` dosyalarında düzenlemeler yapıldı. Bu değerleri `.env` dosyalarınıza eklemeniz gerekiyor.
    1. `node-server` paketinde aşağıdaki değer eklendi.
```
SYSTEM_LANG=""      // Değeri eklendi. Bu değere göre sistem varsayılan dili ayarlanır. Girmek zorundasınız. [tr, en]
```

    2. `front-end` paketinde aşağıdaki değerler eklendi.
```
REACT_APP_JIKAN_INSTANCE_URL    // Eğer JIKAN instance'ı hostluyorsanız, kendi URL'nizi girebilirsiniz. Girmek zorunda değilsiniz.
REACT_APP_DEFAULT_LANG          // Değeri eklendi. Bu değere göre ön yüz varsayılan dili ayarlanır. Girmek zorundasınız. [tr, en]
```
    3. `front-end-admin` paketinde aşağıdaki değerler eklendi.
```
REACT_APP_DEFAULT_LANG          // Değeri eklendi. Bu değere göre ön yüz varsayılan dili ayarlanır. Girmek zorundasınız. [tr, en]
```

5. 3 projedeki paketlerin çoğu güncellendi. Bu yüzden `node-server` servisini çalıştırmadan önce `node_modules` dosyasını silip, `npm install` yapmanız ya da `front-end` veya `front-end-admin` paketlerini buildlemeden önce `node_modules` dosyalarını silip, `yarn install` yapmanız önerilir, yoksa hatalarla karşılaşabilirsiniz.
6. `node-server` içerisinde `metadata` klasörü oluşturduk ama eski serilerin görselleri ne olacak dediğinizi duyar gibiyim. Sıkı tutunun.
    1. [Buradan](https://github.com/ForFansubs/migration-scripts) `migration-scripts` reposunu locale clonelayın.
    2. `node-server` klasörü içerisinden images klasörünü kopyalayıp, `migration-scripts` klasörü içerisindeki `./get-metadata_arts` klasörü içerisine yapıştırın, üstüne yazalım mı diye falan sorarsa evet deyin.
    3. `get-metadata_arts` klasörü içerisindeki `.env.example` klasörünü gerektiği gibi doldurun, `.env` diye kaydedin.
    4. `migration-scripts` içerisinde bir komut ekranı açın. Sırasıyla
```
npm install
cd get-metadata_arts
node get-metadata_arts.js
```
    komutlarını çalıştırın. Bu scriptin database'inizde bulunan bütün seriler için bir metadata resmi oluşturması gerekiyor. Hata falan verirse bakarsınız zaten.
    5. Tamamlandıktan sonra metadata resimlerinizin `./get-metadata_arts/images/metadata` yolunda olması gerekiyor. Bu resimleri kopyalayıp, `node-server` içerisinde `./images/metadata` klasörüne atın.

Eğer bir şeyi unutmadıysam bu adımları uyguladıktan sonra sisteminizin v4'e başarıyla geçmiş olması gerekiyor. Eğer unuttuysam Github'dan dürtün beni. Düzelteyim. Dinlediğiniz için teşekkürler, görüşmek üzere.