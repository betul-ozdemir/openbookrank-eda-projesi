# OpenBookRank Bilimkurgu Kitapları Veri Analizi (EDA)

## 1. Problem
Bu projede OpenBookRank API'si üzerinden bilimkurgu (science-fiction) kategorisindeki kitap verileri çekilerek aşağıdaki üç araştırma sorusuna yanıt aranmıştır:
1. Bilimkurgu okuyucu puanı (`score`) en yüksek 10 kitap hangileridir?
2. Kitapların puanları nasıl bir dağılım göstermektedir?
3. Sıralamada en çok kitabı bulunan yazarlar hangileridir?

## 2. Veri
* **Veri Kaynağı:** OpenBookRank API (`https://openbookrank.com/api/v1/rankings/science-fiction.json`)
* **Veri Çekim Tarihi:** 12 Kasım 2026[cite: 1]
* **Boyut:** Ham veri 805 satır ve 11 sütundan oluşmaktadır[cite: 2].
* **Kullanılan Sütunlar:** `id`, `rank`, `title`, `author`, `year`, `score`, `ratings`

## 3. Yöntem
* `requests` kütüphanesi ile API'den JSON formatında çekilen ham veri `data/raw/science_fiction_raw.json` dosyasına kaydedilmiştir[cite: 1].
* `pandas` ile tablo formatına dönüştürülen veride `title`, `author` ve `score` alanlarında eksik değeri olan satırlar ile tekrar eden `id` kayıtları temizlenmiştir.
* `score` ve `ratings` sütunları sayısal tipe, `year` sütunu tam sayı (`Int64`) tipine dönüştürülerek temiz veri `data/processed/science_fiction_clean.csv` olarak kaydedilmiştir.
* `matplotlib` ve `seaborn` kütüphaneleri kullanılarak her araştırma sorusu için görselleştirmeler üretilmiş ve `figures/` klasörüne kaydedilmiştir.

## 4. Bulgular
* **En Yüksek Puanlı 10 Kitap:** Listede 9.11 puan ile *Light Bringer* (Pierce Brown) ilk sırada yer almaktadır[cite: 2]. (Grafik: `figures/soru1_en_yuksek_puanli_10_kitap.png`)
* **Puan Dağılımı:** Kitapların puan ortalaması `[ortalama değer]`, medyanı ise `[medyan değer]` olarak hesaplanmıştır. (Grafik: `figures/soru2_puan_dagilimi.png`)
* **En Çok Kitabı Bulunan Yazarlar:** Sıralamada en fazla kitabı yer alan yazar `[yazar adı]` (`[kitap sayısı]` kitap) olmuştur. (Grafik: `figures/soru3_en_cok_kitabi_olan_yazarlar.png`)

## 5. Sınırlılıklar
* Veri seti yalnızca OpenBookRank platformundaki bilimkurgu sıralamasıyla sınırlıdır ve farklı platformlardaki okuyucu puanlarını kapsamamaktadır.
* Bazı kitap kayıtlarında yayın yılı (`year`) bilgisi eksik (`NaN`) olduğu için yıl bazlı analizlerde tüm kitaplar yer almamaktadır.

## 6. Çalıştırma
Projeyi yerel ortamınızda çalıştırmak için:
1. Gerekli kütüphaneleri yükleyin:
   ```bash
   pip install -r requirements.txt