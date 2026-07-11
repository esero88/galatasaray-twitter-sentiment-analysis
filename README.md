# Galatasaray Twitter/X Sentiment Analysis

Galatasaray taraftar tabanının takım performansı, transfer kararları ve yönetime karşı Twitter/X üzerindeki genel duygu durumunu (sentiment) veri temelli olarak ölçen bir analiz projesi.

## 🎯 Proje Amacı

Kulüp yönetimi/pazarlama departmanının taraftar algısını güncel ve nesnel verilerle takip edebilmesini sağlamak.

## 🛠️ Kullanılan Araçlar

- **Python** — veri işleme
- **Google Sheets** — raw data depolama
- **Claude + GoFullPage + SmallPDF** — sıfır maliyetli veri toplama
- **BeautifulSoup** — HTML parsing
- **savasy/bert-base-turkish-sentiment-cased** — Türkçe duygu analizi (HuggingFace)
- **Tableau** — interaktif dashboard ve görselleştirme

## 📊 Proje Kapsamı

1. **Veri Toplama:** #Galatasaray, #GS, #CimBom, #ŞampiyonGalatasaray, #UltrAslan, #DursunÖzbekistifa, #HainsinDursunÖzbek hashtag'leriyle son 30 güne ait tweet'lerin toplanması. Orijinal hedef 2.000 tweet olmakla birlikte, manuel/yarı-otomatik toplama yönteminin kısıtları nedeniyle bu hedefin gerçekçi olmadığı tespit edilmiştir; ulaşılabilir ve savunulabilir bir örneklem büyüklüğü hedeflenmekte ve bu durum yönetici özetinde şeffaf biçimde belirtilecektir.

2. **Duygu Analizi:** Tweet'lerin pozitif/negatif/nötr olarak sınıflandırılması; Türkçe'ye özgü dil yapısını (ekleme ekler, argo, kısaltmalar) doğal olarak işleyebilen `savasy/bert-base-turkish-sentiment-cased` modeli kullanılmıştır. Güven skoru 0.65'in altında kalan tahminler "Nötr" olarak etiketlenmiştir.

3. **Görselleştirme:** Sonuçların interaktif bir Tableau dashboard'una dönüştürülmesi.

## 📁 Klasör Yapısı

```
├── data/
│   ├── raw/           # Ham veri (tweets_raw.csv)
│   └── processed/     # Temizlenmiş ve etiketlenmiş veri
├── notebooks/         # Python analiz defterleri (Jupyter)
│   ├── 01_setup.ipynb
│   ├── 02_cleaning.ipynb
│   ├── 03_sentiment.ipynb
│   └── 04_visualization.ipynb
├── outputs/
│   └── figures/       # Grafik çıktıları
└── docs/              # SOW belgesi ve raporlar
```

## 📌 Kapsam Dışı

- Twitter/X dışındaki sosyal medya platformları
- Türkçe dışındaki dillerde yazılmış tweet'ler
- Bireysel kullanıcı profillemesi

## 📄 Lisans

Bu proje [MIT License](LICENSE) ile lisanslanmıştır.

## 🔍 Veri Toplama Metodolojisi

Resmi X (Twitter) API'si artık ücretsiz okuma/arama erişimi sunmadığından (Basic tier aylık ücretli, ücretsiz tier sadece yazma izni veriyor) ve eski ücretsiz scraping araçları (snscrape, Twint) 2023'te X'in altyapı değişiklikleriyle kalıcı olarak bozulduğundan, veri toplama **sıfır maliyetli hibrit bir yöntemle** yapılmıştır:

1. **GoFullPage + SmallPDF:** X arama sayfaları HTML olarak tam sayfa kaydedilmiştir.
2. **BeautifulSoup ile parsing:** Kaydedilen HTML'lerden kullanıcı adı, tweet metni, tarih, beğeni/retweet/yorum/görüntülenme sayıları otomatik çıkarılmıştır.
3. **Google Sheets:** Toplanan ham veri merkezi olarak burada tutulmuş, Python'dan CSV export URL üzerinden çekilmiştir.
4. **Kalite kontrolü:** Alakasız sonuçlar (farklı dilde, konu dışı, spam/bot hesaplar, duplicate kayıtlar, nested/quoted tweet içerikleri) filtrelenmiş; parodi/mizah hesapları `is_parody` sütunuyla etiketlenmiştir.

**Mevcut veri seti:** ~1.239 tweet (veri seti her hafta büyütülmektedir; hedef 1 yıllık veri)

**Bilinen sınırlamalar:**
- X'in "virtualized list" sayfa yapısı nedeniyle tek HTML kaydı başına yalnızca ~9-10 tweet yakalanabilmektedir.
- Bitişik yazılan hashtag'ler (ör. `#dursunözbektransferlernerede`) BERT tarafından doğru sınıflandırılamayabilir; preprocessing iyileştirmesi planlanmaktadır.
- Veri toplama yalnızca son 30 güne ait tweetlerle sınırlıdır.
