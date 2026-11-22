# SebastianMySqlKits

**TR MODDED / Sebastian** tarafından geliştirilen **Unturned (RocketMod)** kit plugini. Oyuncular `/kits` ile kitleri görür, `/kit <ad>` ile yetkileri varsa alır. Kitler ve bekleme süreleri **LiteDB** (varsayılan) ya da **MySQL**'de tutulur; MySQL ile birden çok sunucu aynı kitleri ve beklemeleri paylaşır.

> Bu depo sadece derlenmiş plugini (Releases) ve kullanım bilgisini içerir. Kaynak kod paylaşılmamaktadır.

## Kurulum
1. [Releases](../../releases) sayfasından `SebastianMySqlKits.dll` dosyasını indir, sunucunun `Rocket/Plugins` klasörüne koy.
2. `LiteDB.dll` ve `MySql.Data.dll` dosyalarını (release'te) `Rocket/Libraries` klasörüne koy.
3. Sunucuyu başlat. Ayar dosyası `Rocket/Plugins/SebastianMySqlKits/` altında oluşur. Veritabanı boşsa örnek bir `starter` kiti eklenir.
4. Oyunculara izin ver (`Permissions.config.xml`): `sebastiankits.kits`, `sebastiankits.kit` ve her kit için `kit.<ad>` (ör. `kit.starter`).

## Oyuncu komutları
| Komut | Açıklama |
|---|---|
| `/kits` (`/kitler`) | Kullanabildiğin kitler ve durumları (hazır / kalan süre / tek kullanımlık). |
| `/kit <ad>` | Kiti alır. Envanter doluysa kalan eşyalar yere bırakılır. |

## Yönetim: `/kitadmin` (izin `sebastiankits.admin`)
| Komut | Açıklama |
|---|---|
| `/kitadmin olustur <ad> <süre> [izin]` | Üstündeki eşyalardan (kıyafet, eller, cepler) kit oluşturur. |
| `/kitadmin ekle <ad> <itemId> [miktar]` | Kite eşya ekler. |
| `/kitadmin cikar <ad> <itemId>` | Kitten eşya çıkarır. |
| `/kitadmin cooldown <ad> <süre>` | Bekleme süresi. |
| `/kitadmin izin <ad> <izin \| ->` | Özel izin (`-` = `kit.<ad>`). |
| `/kitadmin aciklama <ad> <metin>` | `/kits` listesinde görünen açıklama. |
| `/kitadmin sil <ad>` / `bilgi <ad>` / `liste` / `yenile` | Silme, ayrıntı, liste, veritabanından yeniden okuma. |
| `/kitadmin sifirla <oyuncu> [kit]` | Oyuncunun bekleme sürelerini sıfırlar. |

**Süre:** `600` (sn), `10m`, `2h`, `1d`, `1d12h`; `0` = beklemesiz, `tek` = tek kullanımlık.

## İzinler
- `kit.<ad>`: o kiti alma. `kit.*`: tüm kitler.
- `sebastiankits.admin`: yönetim + beklemesiz. `sebastiankits.nocooldown`: beklemesiz.

## MySQL
Ayar dosyasında `Veritabani` = `mysql` yap ve `MySql` bölümünü doldur. Tablolar kendiliğinden açılır:
- `<önek>kits`: `Name`, `Cooldown`, `Permission`, `Items` (`itemId:miktar,itemId:miktar`), `Description`. Kitleri doğrudan bu tablodan da düzenleyebilirsin; sunucu 60 sn'de bir yeniden okur.
- `<önek>kit_cooldowns`: `PlayerID`, `Kit`, `LastUsed` (UTC), `Uses`.

Not: MySQL 8 kullanıyorsan veritabanı kullanıcısı `mysql_native_password` ile oluşturulmalı (MariaDB'de sorun yok).

## Lisans
Tüm hakları saklıdır © 2026 Sebastian (TR MODDED). Plugin ücretsiz kullanılabilir; yeniden dağıtımı ve satışı izne tabidir.
