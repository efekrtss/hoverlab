# Katkı rehberi

Teşekkürler! HoverLab'ı daha doğru ve kullanışlı yapmak için her katkı değerli.

## Kataloğa parça eklemek

`src/js/catalog.js` içindeki `RAW` dizisine bir satır ekle:

```js
// [kategori, ad, tipik ağırlık (g), teknik değerler, ek arama kelimeleri]
['motor', '2207 fırçasız 2550KV', 33, {kv:2550, rm:0.05, i0:1.6, imax:50}, '5 inc 4s'],
```

Kategoriye göre teknik değerler:

| Kategori | Alanlar |
|---|---|
| `motor` | `kv` (rpm/V), `rm` (Ω), `i0` (A, boşta), `imax` (A, sürekli) |
| `prop` | `d` (çap, inç), `p` (hatve, inç), `b` (kanat sayısı) |
| `battery` | `chem` (`'lipo'`/`'liion'`), `cells`, `cap` (mAh), `crate` (C), `rint` (paket iç direnci, Ω) |
| `esc` | `esc` (A, motor başına sınır), tekli ESC için `pm:true` |
| `safety` | paraşüt için `chute` (açık alan, m²); diğerleri `null` |
| diğerleri | `null` |

Lütfen pull request açıklamasına değerin **kaynağını** (veri sayfası, kendi ölçümün, test tablosu) yaz. Tahmini değerleri tahmini olarak belirt.

## Çeviri

Arayüz metinleri Türkçe yazılır; İngilizce karşılıkları `src/js/i18n.js` içindeki `EN` sözlüğündedir. Yeni bir metin eklediğinde sözlüğe de ekle. Değişken içeren metinlerde `{}` kullanılır: `'İtki {} g':'Thrust {1} g'`. Parça adlarındaki Türkçe ifadeler `NAME_EN` listesiyle çevrilir.

## Kod değişiklikleri

1. Geliştirirken `src/index.html`'i tarayıcıda aç; değişiklikler yenileyince görünür.
2. Fizik modeline dokunduysan `npm test` çalıştır ve gerekiyorsa `tests/physics.test.mjs`'e test ekle.
3. Açık ve koyu temada, telefon genişliğinde (≈400 px) kontrol et.
4. Bitince `npm run build` çalıştır ve üretilen kök `index.html`'i de commit'e ekle.
5. Renkleri `src/css/style.css` başındaki belirteçlerden (`--accent`, `--ink`…) al; sabit renk yazma.

## Dosya sırası

`src/js/` dosyaları `src/index.html`'de belirli bir sırayla yüklenir ve öncekilerin tanımlarını kullanır:
`core → i18n → catalog → physics → ui → compat → designer → report → compare → flight → scene3d → pid → app`. Yeni dosya eklersen bu sıraya uygun yere koy ve `scripts/build.mjs`'in gömdüğünü kontrol et.

## Fikir listesi

- İngilizce arayüz (çeviri altyapısı)
- Gerçek ölçüm verisiyle pervane katsayısı tablosu (UIUC)
- Açı + hız iç içe (kaskad) PID modu
- Tasarım karşılaştırma görünümü

## Uygunluk kuralları

Parça uyumu denetimleri `src/js/compat.js` içindedir. Yeni bir gövde ya da ESC eklerken `FRAME_INFO` (en büyük pervane, kol sayısı) ve `ESC_INFO` (hücre aralığı, fırçalı/fırçasız, kanal sayısı) tablolarına da satır ekle. Metinler `tl('Türkçe', 'English')` ile iki dilde yazılır.
