# Changes from Upstream (Appétit)

This is a fork of [Appétit](https://github.com/f/appetit) by [Fatih Kadir Akın (FKA)](https://github.com/f).  
Below are all the changes and additions made in this fork.

---

## 1. Kişiselleştirme / Branding

- Site başlığı `Appétit — FKA Apps` → `kocdev — Apps by Osman Koç` olarak değiştirildi.
- Meta description, canonical URL (`apps.osmankoc.dev`) ve CNAME güncellendi.
- Sidebar'daki geliştirici bilgisi (isim, avatar, bağlantı) Osman Koç olarak güncellendi.
- Mobil üst bar başlığı `Appétit` → `kocdev` olarak değiştirildi.
- Logo (`logo.svg`), özel bir SVG ile değiştirildi; ek olarak `logo.png` ve `logo-oval.svg` eklendi.
- `apps.json` içindeki `store` metadata'sı (name, developer, tagline, url, github) kocdev/osmankoc bilgileriyle güncellendi.

---

## 2. Kategori Sistemi Yenilendi

Upstream'deki `macOS` ve `CLI` kategorileri kaldırılarak yerine daha kapsamlı kategoriler eklendi:

| Eklenen Kategoriler  | Kaldırılan Kategoriler |
|----------------------|------------------------|
| Utilities            | macOS Apps             |
| Lifestyle            | CLI Apps               |
| Health & Fitness     |                        |
| Entertainment        |                        |

- Her yeni kategori için sidebar'a SVG ikon eklendi (`utilities`, `productivity`, `lifestyle`, `health-fitness`, `entertainment`).
- Discover (Keşfet) sayfasında her yeni kategoriye ait "section" (bölüm) render edilmesi sağlandı.
- `apps.json` içindeki categories dizisi ve her uygulamanın `category` alanı yeni yapıya göre güncellendi.

---

## 3. Mobil Uygulamalar için Çoklu Link Desteği (App Store / Google Play)

Upstream'de her uygulamanın yalnızca tek bir `homepage` veya `downloadUrl` bağlantısı vardı. Bu fork'ta mobil uygulamaların hem App Store hem de Google Play linklerini taşıyabilmesi için yeni bir `links` alanı eklendi.

### apps.json — Yeni `links` alanı

```json
"links": [
  { "label": "App Store", "url": "https://apps.apple.com/...", "platform": "ios" },
  { "label": "Google Play", "url": "https://play.google.com/...", "platform": "android" }
]
```

### Uygulama Kartı / Satırı — "Get" Butonu Davranışı

- `links` dizisi dolu olan uygulamalarda "Get" butonuna tıklanınca artık platform seçim modalı (veya dropdown) açılıyor.
- Daha önce yalnızca tek bir URL'ye yönlendirme yapılıyordu.
- `getButtonLabel()` fonksiyonu güncellendi: `links` dizisi varsa veya kategori `games`/`entertainment` ise buton etiketi `"Get"` döner.

### App Detail — Platform Dropdown

Uygulama detay ekranında, `links` dizisi dolu olan uygulamalar için "Get" butonu; altında **açılır dropdown** (platform listesi) gösteren bir yapıya dönüştürüldü.

- `get-dropdown-wrapper` / `get-dropdown` CSS sınıfları eklendi.
- Her platform bağlantısı; platforma özgü icon (iOS/Android SVG), etiket ve ok ikonuyla listeleniyor.
- Dropdown, dışarıya tıklanınca veya `Escape` tuşuna basılınca kapanıyor.

### App Row / Kart — Tıklanma Davranışı

- Uygulama satırına veya kartına tıklanınca app detail ekranına gidilmemesi için `get-dropdown` tıklamaları olaylardan muaf tutuldu (`stopPropagation`).

### Platform Seçim Modalı (`showLinksModal`)

Ana uygulama listesindeki "Get" butonuna tıklanınca (`app.links` varsa) yeni bir **modal ekranı** açılıyor:

- Modal'da uygulama ikonu ve adı gösteriliyor.
- Her platform linki; `.modal-platform-link` elemanı olarak, platforma özgü icon ve ">" oku ile listeleniyor.
- Mevcut `closeModal()` altyapısı kullanılıyor.

### Yeni `platformIcon(platform)` Fonksiyonu

`"ios"`, `"android"` ve genel harici link olmak üzere 3 farklı SVG ikonu döndüren yardımcı fonksiyon eklendi.

---

## 4. Yeni CSS Sınıfları (style.css)

| Sınıf / Grup                  | Açıklama                                                        |
|-------------------------------|-----------------------------------------------------------------|
| `.platform-links`             | Detay ekranında platform butonlarının wrapper'ı                 |
| `.platform-link-btn`          | Yuvarlak kenarlıklı platform butonu                             |
| `.modal-platform-links`       | Modal içindeki platform linkleri listesi                        |
| `.modal-platform-link`        | Tek bir platform link satırı                                    |
| `.modal-platform-icon`        | Platform ikonunun kapsayıcısı                                   |
| `.modal-platform-label`       | Platform etiketi                                                |
| `.modal-platform-chevron`     | Platform satırı ok ikonu                                        |
| `.get-dropdown-wrapper`       | Detay sayfasındaki dropdown'ın konumlandırma wrapper'ı          |
| `.get-dropdown`               | Dropdown panel (opacity/transform animasyonlu)                  |
| `.get-dropdown.open`          | Açık dropdown durumu                                            |
| `.get-dropdown-item`          | Dropdown içindeki tek bir link satırı                           |
| `.get-dropdown-icon`          | Dropdown satırındaki platform ikonu kapsayıcısı                 |
| `.get-dropdown-label`         | Dropdown satırı etiketi                                         |
| `.get-dropdown-arrow`         | Dropdown satırı ok ikonu                                        |

---

## 5. Layout ve Responsive Düzeltmeler

- `body` ve `.app-store`'dan `overflow: hidden` kaldırıldı → sayfa kayması sorunu çözüldü.
- `width: 100vw` → `width: 100%`, `max-width: 100vw` → `max-width: 100%` olarak değiştirildi (yatay taşma önlendi).
- `.info-grid` ve `.app-detail` üzerindeki `overflow: hidden` mobil breakpoint'te kaldırıldı.
- App detail actions alanı mobilde ortalandı (`justify-content: center`).

---

## 6. App Detail — Koşullu Render İyileştirmeleri

- GitHub linki (`View on GitHub`) yalnızca `app.github` değeri varsa gösteriliyor.
- "Source Code" bilgi satırı yalnızca `app.github` değeri varsa gösteriliyor.
- `getButtonLabel()` mantığı genişletildi; `app.downloadUrl` de fallback olarak destekleniyor.

---

## 7. Uygulama Kataloğu (apps.json)

Upstream'deki uygulamalar tamamen kaldırılarak Osman Koç'un kendi projeleri eklendi:

| Uygulama                    | Platform          | Özellik                                      |
|-----------------------------|-------------------|----------------------------------------------|
| **ColdCase**                | iOS & Android     | App Store + Google Play linkleri             |
| **yâdet**                   | iOS & Android     | App Store + Google Play linkleri             |
| **Whistle SOS**             | iOS & Android     | App Store + Google Play linkleri             |
| **Git Search AI**           | VS Code           | VS Code Marketplace                          |
| **GuidGenerator**           | VS Code           | VS Code Marketplace                          |
| **GuidGenerator for VS**    | Visual Studio     | Visual Studio Marketplace                    |
| **Personal Website**        | Web               | osmankoc.dev                                 |
| **En Yakın Hastaneyi Bul**  | Telegram Bot      | GitHub açık kaynak                           |
| **En Yakın Eczaneyi Bul**   | Telegram Bot      | GitHub açık kaynak                           |

Featured banner 3 uygulamayla güncellendi: ColdCase, yâdet, Git Search AI.

---

## 8. README.md Güncellemeleri

- Fork attribution (kaynak belirtme) açıkça eklendi.
- "What's different from upstream" bölümü eklendi.
- Clone URL ve tüm linkler bu fork'a göre güncellendi.
- `apps.json` örnek içeriği yeni platform/kategori yapısına göre revize edildi.

---

## 9. Diğer

- `update-stats.sh` ve GitHub Actions workflow'u bu fork'un repository'sine göre güncellendi.
- Upstream `apps.js` dosyası kaldırıldı; uygulama verisi yalnızca `apps.json` üzerinden yönetiliyor.
