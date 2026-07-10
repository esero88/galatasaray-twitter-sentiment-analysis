# Galatasaray Twitter/X Sentiment Analysis

Galatasaray taraftar tabanının takım performansı, transfer kararları ve yönetime karşı Twitter/X üzerindeki genel duygu durumunu (sentiment) veri temelli olarak ölçen bir analiz projesi.

## 🎯 Proje Amacı

Kulüp yönetimi/pazarlama departmanının taraftar algısını güncel ve nesnel verilerle takip edebilmesini sağlamak.

## 🛠️ Kullanılan Araçlar

- **Python** — veri işleme
- **Google Sheets** — raw data
- **Claude** — veri toplama
- **VADER / TextBlob** — duygu analizi (sentiment analysis)
- **Tableau / Power BI** — interaktif dashboard ve görselleştirme

## 📊 Proje Kapsamı

1. **Veri Toplama:** #Galatasaray, #GS, #CimBom, #ŞampiyonGalatasaray, #UltrAslan, #DursunÖzbekistifa, #HainsinDursunÖzbek hashtag'leriyle son 30 güne ait tweet'lerin toplanması. Orijinal hedef 2.000 tweet olmakla birlikte, manuel/yarı-otomatik toplama yönteminin kısıtları nedeniyle bu hedefin gerçekçi olmadığı tespit edilmiştir; ulaşılabilir ve savunulabilir bir örneklem büyüklüğü hedeflenmekte ve bu durum yönetici özetinde şeffaf biçimde belirtilecektir.
2. **Duygu Analizi:** Tweet'lerin pozitif/negatif/nötr olarak sınıflandırılması
3. **Görselleştirme:** Sonuçların interaktif bir dashboard'a dönüştürülmesi

## 📁 Klasör Yapısı

```
├── data/          # Ham ve işlenmiş veri
├── notebooks/     # Python analiz defterleri (Jupyter)
├── scripts/       # Veri toplama ve analiz scriptleri
├── dashboard/     # Tableau/Power BI dosyaları
└── docs/          # SOW belgesi ve raporlar
```

## 📌 Kapsam Dışı

- Twitter/X dışındaki sosyal medya platformları
- Türkçe dışındaki dillerde yazılmış tweet'ler
- Bireysel kullanıcı profillemesi

## 📄 Lisans

Bu proje [MIT License](LICENSE) ile lisanslanmıştır.

## 🔍 Veri Toplama Metodolojisi

Resmi X (Twitter) API'si artık ücretsiz okuma/arama erişimi sunmadığından (Basic tier aylık ücretli, ücretsiz tier sadece yazma izni veriyor) ve eski ücretsiz scraping araçları (snscrape, Twint) 2023'te X'in altyapı değişiklikleriyle kalıcı olarak bozulduğundan, veri toplama **manuel + yarı otomatik hibrit bir yöntemle** yapılmıştır:

1. **Manuel küratörlük:** #Galatasaray, #GS, #CimBom, #ŞampiyonGalatasaray, #UltrAslan, #DursunÖzbekistifa, #HainsinDursunÖzbek aramaları X'in "En Yeni" (Latest) sekmesinde yapılmış, alakalı tweetler elle seçilip Google Sheets'e aktarılmıştır.
2. **Yarı otomatik çıkarım:** Arama sonuçları sayfası HTML olarak kaydedilip Python (BeautifulSoup) ile parse edilerek kullanıcı adı, tweet metni, tarih, beğeni/retweet/yorum/görüntülenme sayıları otomatik çıkarılmıştır.
3. **Kalite kontrolü:** Alakasız sonuçlar (farklı dilde, konu dışı, çok eski tarihli tweetler, rakip takım haberleri, anma/taziye mesajları, spam/bot hesaplar, nested/quoted tweet içerikleri, duplicate kayıtlar) elle filtrelenmiş; parodi/mizah hesapları (`is_parody` sütunu, 0/1 olarak) ayrıca etiketlenmiştir.

**Bilinen sınırlamalar:**

- X'in sayfa yapısı "virtualized list" kullandığından (scroll ettikçe eski tweetler bellekten silindiğinden), tek bir HTML kaydı başına yalnızca ~9-10 tweet yakalanabilmektedir; büyük hacimli veri için tekrarlanan kayıt + parse döngüsü gerekmiştir.
- SOW'da hedeflenen 2.000 tweet yerine, bu yöntemle toplanabilen gerçekçi bir örneklem (proje sonunda kesinleşecek) kullanılmıştır. Bu, raporun "Yönetici Özeti" bölümünde açıkça belirtilecektir.
- Veri toplama yalnızca son 30 güne ait tweetlerle sınırlıdır; göreceli zamanlar (5s/3d/1sa vb.) ve kısaltılmış tarihler ("X Tem" gibi) gerçek tarihe çevrilerek kaydedilmiştir.
