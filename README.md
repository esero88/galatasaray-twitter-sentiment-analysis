# Galatasaray Twitter/X Sentiment Analysis

Galatasaray taraftar tabanının takım performansı, transfer kararları ve yönetime karşı Twitter/X üzerindeki genel duygu durumunu (sentiment) veri temelli olarak ölçen bir analiz projesi.

## 🎯 Proje Amacı

Kulüp yönetimi/pazarlama departmanının taraftar algısını güncel ve nesnel verilerle takip edebilmesini sağlamak.

## 🛠️ Kullanılan Araçlar

- **Python** — veri toplama ve işleme
- **VADER / TextBlob** — duygu analizi (sentiment analysis)
- **Tableau / Power BI** — interaktif dashboard ve görselleştirme

## 📊 Proje Kapsamı

1. **Veri Toplama:** #Galatasaray, #GS anahtar kelimeleriyle son 30 güne ait en az 2.000 tweet'in toplanması
2. **Duygu Analizi:** Tweet'lerin pozitif/negatif/nötr olarak sınıflandırılması
3. **Görselleştirme:** Sonuçların interaktif bir dashboard'a dönüştürülmesi

## 📁 Klasör Yapısı

├── data/          # Ham ve işlenmiş veri
├── notebooks/     # Python analiz defterleri (Jupyter)
├── scripts/       # Veri toplama ve analiz scriptleri
├── dashboard/     # Tableau/Power BI dosyaları
└── docs/          # SOW belgesi ve raporlar

## 📌 Kapsam Dışı

- Twitter/X dışındaki sosyal medya platformları
- Türkçe dışındaki dillerde yazılmış tweet'ler
- Bireysel kullanıcı profillemesi

## 📄 Lisans

Bu proje [MIT License](LICENSE) ile lisanslanmıştır.
