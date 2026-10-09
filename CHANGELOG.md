# Değişiklik günlüğü

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
