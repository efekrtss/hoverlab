# Değişiklik günlüğü

## 2.7.0 — kalite turu
- **Erişilebilirlik (WCAG AA):** açık temada kırmızı, yeşil, turuncu ve turkuaz tonları okunabilirlik eşiğine (4,5:1) göre koyulaştırıldı;
  sayfaya ana bölge (`main`), "İçeriğe geç" bağlantısı, panellerde doğru diyalog yapısı ve odak tuzağı (Tab panelden çıkmaz, kapanınca odak düğmeye döner),
  kaydırılabilir tablo ve kod alanlarına klavye erişimi, boş tablo başlıklarına ekran okuyucu metni eklendi. axe-core denetimi açık ve koyu temada, masaüstü ve 320 px'te ihlalsiz
- **Paylaşım önizlemesi:** `og.png` kapak görseli, kanonik adres, og:url / og:image / Twitter kartı; tema rengi yeni renklerle uyumlu
- Akıllı tasarımcı: "çok ağır" nedeniyle sonuç çıkmadığında açıklama gösterilmiyordu (düzeltildi)
- JavaScript kapalıysa uyarı
- Denetlendi: tüm sekme, şablon, panel ve senaryolarda konsol hatası yok; 320–1280 px arası taşma yok; İngilizce modda çevrilmemiş metin yok;
  tarayıcı deposu kapalıyken, 3B kütüphanesi yüklenemezken, geçersiz girişlerde ve zararlı içe aktarma metninde site çalışmaya devam ediyor

## 2.6.0
- **Tasarım karşılaştırma** (TR/EN): en fazla 3 tasarımı yan yana koyar (ağırlık, itki, itki/ağırlık, hover gazı, uçuş süresi, verim, akım, risk puanı, ana parçalar);
  her satırda en iyi değer işaretlenir, itki eğrileri ve ağırlık çizgileri tek grafikte üst üste çizilir, kısa bir yorum yazılır
- Karşılaştırmaya ekleme: parça listesinin altındaki "+ Karşılaştır", "Tasarımlarım" listesindeki "Karşılaştır", Akıllı tasarımcıda "Karşılaştırmaya ekle" ve "Bu 3 öneriyi karşılaştır"
- Liste dolunca ekranın altında "Karşılaştır (n)" düğmesi çıkar; liste tarayıcıda saklanır
- Kontroller listesi ayrı bir fonksiyona taşındı (karşılaştırma ekranı aynı kuralları kullanıyor)

## 2.5.0
- **Akıllı tasarımcı** (TR/EN): boyut, kullanım amacı (yarış, genel, uzun uçuş, yük taşıma), motor sayısı, en az uçuş süresi, ek yük ve batarya türüne göre
  katalogdaki gövde–motor–pervane–batarya–ESC kombinasyonlarını fizik modeliyle tarar; uyumluluk denetiminden geçen en iyi 3 tasarımı önerir ve tek tıkla yükler.
  Gerçekçilik sınırları: gövde sınıfına göre en büyük kalkış ağırlığı, batarya payı ≤ %50, motor akımı, pervane ucu hızı, batarya C değeri
- **Dışa aktarma:** yazdırılabilir tasarım raporu (PDF olarak kaydedilir: parça listesi, teknik değerler, çalışma noktaları, eğri grafiği, kontroller, uygunluk)
  ve CSV parça listesi (Excel için Türkçede noktalı virgül, İngilizcede virgül ayraçlı)
- Arama sırasında 3B sahne duraklatılır (daha hızlı sonuç)

## 2.4.1
- Depo gizli (private) yapıldı; lisans "Tüm hakları saklıdır" olarak değişti. Sitedeki "açık kaynak" ifadeleri ve kaynak kodu bağlantısı kaldırıldı
- Uygunluk yan sekmesi yalnızca çok geniş ekranlarda (≥1440 px) görünür; içerikle çakışmıyor

## 2.4.0
- **Uygunluk paneli** (yan panel, TR/EN): uçuş riski puanı, "Uçuşa hazır mı?" listesi (gövde, motor, pervane, ESC, kontrolcü, IMU, kumanda bağlantısı, batarya) ve parça uyumu denetimleri:
  gövde ↔ pervane ölçüsü ve kol sayısı, motor ↔ batarya gerilimi, motor ↔ pervane yükü, ESC ↔ motor tipi (fırçalı/fırçasız), batarya ↔ ESC gerilim aralığı,
  ESC kanal sayısı ve akım sınıfı, kontrolcü ↔ ESC yığın ölçüsü, otopilot ↔ GPS, Bluetooth menzili, batarya ağırlık payı, 250 g sınıfı
- Uçuş öncesi kontrol listesi
- Aramada gövdeler en büyük pervane ölçüsü ve kol sayısıyla listeleniyor
- Heksa taşıyıcı şablonu 680 mm gövdeye geçti (550 mm gövdeye 12" pervane sığmıyordu)
- Kontroller listesindeki durum simgeleri yeniden renkli
- Dil düğmesinde bayraklar; sekme başlığı yalnızca "HoverLab"

## 2.3.0
- Yeni ad: **HoverLab** (eski adı İtkiLab)
- İngilizce arayüz: dil düğmesi, tarayıcı diline göre otomatik seçim, İngilizce sayı biçimi, İngilizce ESP32 kod yorumları
- Katalog ~170 → ~300 parça (whoop'tan 12S tarım dronlarına)
- "PID nedir?" paneli: tarihçe (Watt, Maxwell, Minorsky, Ziegler–Nichols), P/I/D'nin anlamı, drone için önemi, canlı P / PD / PID karşılaştırması, ayar adımları ve sık hatalar

## 2.2.1
- Ayarlanabilir maksimum eğim açısı (5–45°) ve isteğe bağlı eğimde gaz telafisi (1/cos θ)
- Kuvvet şeması drone'u gerçek açısıyla çiziyor (önceden 0,8 katı çiziliyordu); itkinin dikey/yatay bileşenleri, θ açısı ve ağırlıkla karşılaştırma gösteriliyor
- Kontroller listesine "eğilme payı": tam gazda irtifa kaybetmeden çıkılabilecek en büyük açı

## 2.2.0
- Yeni görünüm: kırmızı vurgulu tema, Baloo 2 + Nunito yazı tipleri, yuvarlak hatlar, maskot
- Arıza ve güvenlik senaryoları: pervane kırma, güvenli iniş, eve dönüş, sinyal kaybı, düşük batarya inişi, paraşüt; iniş hızı değerlendirmesi
- Drone tipine göre arıza toleransı (kuad 0, heksa 1, okta 2) ve Kontroller listesinde tolerans/paraşüt denetimi
- Katalog 85 → 170 parça; yeni kategori: Güvenlik
- Yeni şablonlar: Heksa taşıyıcı, Okta ağır yük
- 3B: iniş takımı, gimbal, paraşüt, kırık pervane parçaları, takla
- GitHub Pages'te yayın: https://efekrtss.github.io/hoverlab/

## 2.1.1
- Kök `index.html` artık tek başına çalışıyor (zip içinden ya da önizlemede açılınca bozuk görünme sorunu giderildi); kaynaklar `src/` altına taşındı

## 2.1.0
- PID ayar laboratuvarı: tek eksen simülasyonu, otomatik ayar, ESP32 + MPU-6050 kod üretici
- Kayıtlı tasarımlar ve paylaşım bağlantısı
- Hafif mod (zayıf cihazlarda kendiliğinden)
- Grafikte fareyle değer okuma, sekmelerde klavye ile gezinme
- İçe aktarılan ve paylaşılan verilerin doğrulanması
- Açık kaynak yapı: ayrı dosyalar, testler, GitHub Pages iş akışı, tek dosya derleyici

## 2.0.0
- Bileşen kataloğu ve arama
- Yeniden tasarlanan arayüz ve 3B sahne (gölgeler, burgulu pervaneler, sahne objeleri)

## 1.0.0
- İlk sürüm: itki hesaplayıcı ve dikey uçuş simülasyonu
