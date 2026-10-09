# HoverLab

**Drone'unu tasarla, uçur, ölç, PID'ini ayarla.**

**Canlı site:** https://efekrtss.github.io/hoverlab/

HoverLab, tarayıcıda çalışan açık kaynak bir drone tasarım aracıdır. Bileşenleri seçersin; itki, akım, hover gazı ve uçuş süresi anında hesaplanır. Drone aynı fizikle 3B sahnede uçar. PID laboratuvarı tasarımına göre kazanç önerir ve ESP32 + MPU-6050 başlangıç kodu üretir.

Sunucu ya da veritabanı yoktur. Kök klasördeki `index.html` tek başına çalışan hazır sayfadır: çift tıklayıp açman yeterli.

## Özellikler

- **Drone'unu oluştur:** yaklaşık 300 parçalık katalogda arama (motor, pervane, batarya, ESC/sürücü, kontrolcü, sensör, video, alıcı). Motor, pervane ya da batarya eklenince teknik değerler kendiliğinden dolar; ağırlıkları kendi ölçtüğün değerle değiştirebilirsin.
- **Hesaplar:** itki/ağırlık oranı, hover gazı, hover uçuş süresi, gaz–itki–akım eğrisi, ESC ve batarya yük kontrolleri, gerilim düşümü, pervane ucu hızı.
- **3B uçuş sahnesi:** gaz ve eğim kontrolü, takip ve gözlemci kamerası, itki okları, zayıf cihazlar için hafif mod. Model listendeki parçalara göre değişir (kamera, GPS, anten, batarya boyu).
- **Arıza ve güvenlik senaryoları:** pervane kırma, güvenli iniş, eve dönüş, sinyal kaybı (yerinde in / eve dön / motorları kapat), düşük bataryada otomatik iniş ve paraşüt. Sonuç drone tipine göre değişir: kuad tek pervane kaybında düşer, heksa 1, okta 2 kaybı tolere eder.
- **İki dil:** Türkçe ve İngilizce arayüz; sağ üstteki düğmeyle değişir, tarayıcı diline göre otomatik seçilir. Çeviriler `src/js/i18n.js` içinde.
- **PID ayar laboratuvarı:** tek eksen (roll) simülasyonu; ağırlık merkezi kayması, rüzgâr darbesi, sensör gürültüsü ve gecikmesi dahil. Otomatik ayar, ESP32 kod üretici ve PID'i tarihçesinden ayar adımlarına kadar anlatan açılır panel ("PID nedir?").
- **Kaydet ve paylaş:** tasarımlar tarayıcıda saklanır; bağlantı ya da metin olarak paylaşılır. Hiçbir veri sunucuya gitmez.

## Hızlı başlangıç

```bash
git clone https://github.com/efekrtss/hoverlab.git
cd hoverlab
# index.html'i tarayıcıda aç. Hepsi bu.
# Geliştirirken src/index.html'i aç: kaynak dosyaları doğrudan yükler.
```

Testleri çalıştırmak ve tek dosyalık sürüm üretmek için Node.js 18+ gerekir (ek paket yok):

```bash
npm test          # fizik modeli testleri
npm run build     # src/ → index.html (yayın sayfası) ve dist/hoverlab-offline.html (internetsiz)
```

## Yayına alma

**GitHub Pages:** Depoyu GitHub'a yükle, *Settings → Pages → Deploy from a branch → `main` / `(root)`* seç. Kök `index.html` hazır olduğu için derleme gerekmez. `.github/workflows/ci.yml` her gönderimde testleri çalıştırır ve `index.html`'in güncel olduğunu kontrol eder.

**Netlify / Cloudflare Pages:** Klasörü olduğu gibi sürükle-bırak; derleme komutu gerekmez.

Kendi kopyanı yayınlıyorsan `src/js/app.js` başındaki `SITE_URL` ve `REPO_URL` değerlerini doldurup `npm run build` çalıştır: paylaşım bağlantıları doğru adrese gider, alt bilgide kaynak kodu bağlantısı görünür.

## Klasör yapısı

```
index.html              Yayın sayfası (üretilir; doğrudan düzenleme)
src/index.html          Geliştirme sayfası: kaynakları ayrı ayrı yükler
src/css/style.css       Tüm stiller (açık/koyu tema belirteçleri en üstte)
src/js/core.js          Ortak yardımcılar
src/js/catalog.js       Bileşen kataloğu ve hazır şablonlar  ← parça eklemek için burası
src/js/physics.js       Motor–pervane–batarya modeli (DOM kullanmaz, test edilir)
src/js/ui.js            Tasarım arayüzü, arama, sonuçlar, grafik
src/js/flight.js        Uçuş dinamiği
src/js/scene3d.js       3B sahne ve 2B kuvvet şeması
src/js/pid.js           PID laboratuvarı ve ESP32 kod üretici
src/js/app.js           Döngü, kayıt, paylaşım, başlatma
vendor/                 three.js r128 (MIT)
assets/                 Simge
tests/                  node --test ile çalışan fizik testleri
scripts/build.mjs       src/ → index.html ve dist/hoverlab-offline.html
```

Kaynaklar sırayla yüklenen klasik `<script>` dosyalarıdır; `src/index.html` da derleyici olmadan, `file://` üzerinden açılır. Bir şey değiştirdiğinde `npm run build` ile kök `index.html`'i yeniden üret; GitHub iş akışı bunun unutulmadığını kontrol eder.

## Model nasıl hesaplıyor?

- **Motor:** DC motor eşdeğer devresi, `I = (V − ω/Kv) / Rm`, tork `Q = (I − I₀) / Kv`. Motor torku pervanenin istediği torka eşitlenene kadar devir aranır.
- **Pervane:** `T = Cₜ·ρ·n²·D⁴`, `P = Cₚ·ρ·n³·D⁵`. Katsayılar girilmezse hatve/çap oranı ve kanat sayısından tahmin edilir.
- **Batarya:** açık devre gerilimi eksi iç direnç düşümü; gaz oranı ortalama motor gerilimini belirler.
- **Hava:** rakım ve sıcaklıktan yoğunluk (ISA).
- **PID:** tasarımın ataleti, kol uzunluğu, motor tepki süresi ve gerçek itki eğrisiyle tek eksen benzetimi.

## Sınırlar

Bu bir tahmin aracıdır, ölçüm cihazı değildir.

- Pervane katsayısı girilmezse itki ±%20 sapabilir. En doğru sonuç için UIUC veya üretici pervane verisini gir.
- Sonuçlar statik itkidir; ileri uçuşta ve rüzgârda itki azalır. Uçuş süresi yalnızca sabit hover içindir.
- Katalogdaki ağırlıklar ve motor değerleri tipik değerlerdir, belirli bir ürünün ölçümü değildir.
- PID modeli tek eksenli ve basitleştirilmiştir. Üretilen kod bir başlangıç noktasıdır: ilk testleri kazançların yarısıyla ve **pervanesiz** yap.

## Katkı

Katkılar memnuniyetle karşılanır. En kolay başlangıç kataloğa doğrulanmış parça eklemektir. Ayrıntılar: [CONTRIBUTING.md](CONTRIBUTING.md).

## Lisans

[MIT](LICENSE). three.js kendi MIT lisansıyla `vendor/` altında dağıtılır.

---

### English summary

HoverLab is an open-source, in-browser drone design tool: pick components from a searchable catalog, get thrust-to-weight, hover throttle, current and flight time instantly, fly the build in a 3D scene, and tune a single-axis PID loop that generates ESP32 + MPU-6050 starter code. No server or build step; open `index.html`. The interface is available in Turkish and English (toggle at the top right); more translations are welcome.
