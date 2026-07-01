# Prompt Günlüğü

Bu dosya, proje geliştirme sürecinde bir yapay zekâ kodlama asistanına verilen önemli promptları kronolojik sırayla ve kullanıldıkları adımla birlikte özetler. Her promptun tam metni `prompts/prompt_01_*.txt ... prompt_12_*.txt` dosyalarında saklanmaktadır; burada yalnızca amaç ve üretilen çıktı özetlenmiştir.

## 1. Prompt — Proje klasör yapısı
- Adım: Çalışma alanı kurulumu
- Amaç: Proje kök klasöründe standart klasör yapısını oluşturmak.
- Kısa özet: `data/raw`, `data/processed`, `notebooks`, `outputs/figures`, `outputs/tables`, `reports`, `prompts` klasörlerini oluştur; durum ve değişiklik günlüğü dosyalarını başlat.
- Üretilen çıktı: Proje klasör iskeleti (`data/`, `notebooks/`, `outputs/`, `reports/`, `prompts/`).

## 2. Prompt — Ham veri setinin bulunması ve kopyalanması
- Adım: Veri seti envanteri
- Amaç: Online Retail II ham veri dosyasını tespit edip `data/raw/` içine kopyalamak.
- Kısa özet: Kök klasördeki veri dosyasını (.csv/.xlsx) bul, standart bir adla `data/raw/` altına kopyala, orijinali değiştirme.
- Üretilen çıktı: `data/raw/online_retail_ii.csv`.

## 3. Prompt — Proje metadata dosyaları
- Adım: Temel dokümantasyon
- Amaç: Projenin devamı için gerekli minimum metadata dosyalarını oluşturmak.
- Kısa özet: `requirements.txt` (pandas, numpy, matplotlib, seaborn, scikit-learn, openpyxl, jupyter), ilk `README.md` ve prompt kayıt dosyasını oluştur.
- Üretilen çıktı: `requirements.txt`, `README.md`.

## 4. Prompt — Notebook iskeleti
- Adım: Ana not defteri iskeleti
- Amaç: Analiz not defterinin bölüm başlıklarını ve import hücresini oluşturmak.
- Kısa özet: `notebooks/online_retail_project.ipynb` dosyasını oluştur; genel bakış, import, ham veri yükleme, inceleme başlıklarını ekle; pandas/numpy/matplotlib/seaborn importla.
- Üretilen çıktı: Başlangıç notebook iskeleti.

## 5. Prompt — Ham veri yükleme ve ilk inceleme
- Adım: Veri yükleme
- Amaç: Ham veriyi `df`'e yüklemek ve ilk incelemeyi yapmak.
- Kısa özet: Veriyi yükle; `shape`, `head`, `tail`, `info`, `describe`, eksik değer ve tekrar kayıt sayımlarını ekle; beklenen sütunları not düş.
- Üretilen çıktı: Notebook veri yükleme ve inceleme hücreleri (1.067.371 satır, 8 sütun).

## 6. Prompt — Temizleme teşhisi
- Adım: Temizleme öncesi teşhis
- Amaç: Temizlenecek sorunları saymak ve bir özet tablo üretmek.
- Kısa özet: Eksik CustomerID/Description, tam tekrar satırlar, iptal faturaları (InvoiceNo "C"), Quantity<=0 ve UnitPrice<=0 kayıtlarını say; oran tablosunu kaydet.
- Üretilen çıktı: `outputs/tables/cleaning_summary.csv`.

## 7. Prompt — Temizlenmiş veri setinin oluşturulması
- Adım: Veri temizleme
- Amaç: EDA ve modelleme için temizlenmiş işlem düzeyinde veri seti üretmek.
- Kısa özet: Eksik CustomerID, iptal faturaları, pozitif olmayan Quantity/UnitPrice ve tekrar satırları çıkar; `TotalPrice = Quantity * UnitPrice` oluştur; temiz veriyi kaydet.
- Üretilen çıktı: `data/processed/online_retail_cleaned.csv` (779.425 satır).

## 8. Prompt — EDA: satış ve ülke analizi
- Adım: Keşifsel veri analizi (1)
- Amaç: Zaman içindeki satış trendi ve ülke bazlı geliri yanıtlamak.
- Kısa özet: Aylık toplam gelir ve fatura sayısı tablosunu ve çizgi grafiğini üret; en yüksek gelirli 10 ülkeyi çubuk grafikle göster.
- Üretilen çıktı: `monthly_sales_summary.csv`, `top_countries_revenue.csv`, `monthly_revenue_trend.png`, `top_countries_revenue.png`.

## 9. Prompt — EDA: ürün ve sayısal değişken analizi
- Adım: Keşifsel veri analizi (2)
- Amaç: Ürün gelirini ve sayısal sipariş davranışını yanıtlamak.
- Kısa özet: En yüksek gelirli 10 ürün tablosunu ve çubuk grafiğini üret; Quantity/UnitPrice/TotalPrice için özet istatistik, histogram ve korelasyon ısı haritası oluştur.
- Üretilen çıktı: `top_products_revenue.csv`, `numeric_summary.csv`, `top_products_revenue.png`, `totalprice_distribution.png`, `numeric_correlation_heatmap.png`.

## 10. Prompt — RFM özellik mühendisliği
- Adım: Özellik mühendisliği
- Amaç: Müşteri düzeyinde Recency, Frequency, Monetary özellikleri oluşturmak.
- Kısa özet: Referans tarih = son fatura tarihi + 1 gün; Recency = son alışverişten bu yana geçen gün; Frequency = tekil fatura sayısı; Monetary = toplam harcama. Tabloyu kaydet.
- Üretilen çıktı: `outputs/tables/rfm_features.csv` (5.878 müşteri).

## 11. Prompt — K-Means müşteri segmentasyonu
- Adım: Modelleme (kümeleme)
- Amaç: RFM özellikleriyle basit ve savunulabilir bir K-Means modeli eğitmek.
- Kısa özet: RFM'yi `log1p` + StandardScaler ile ölçekle; k=2–6 için inertia ve silhouette hesapla; savunulabilir k seç; final modeli `random_state=42` ile eğit; segment tablosunu ve görselleri kaydet.
- Üretilen çıktı: `clustering_metrics.csv`, `cluster_summary.csv`, `customer_segments.csv`, elbow/silhouette ve RFM kümeleme görselleri (k=4).

## 12. Prompt — Teslim destek dosyaları
- Adım: Sonuç konsolidasyonu ve dokümantasyon
- Amaç: Sonuçları rapor yazımına uygun özet tablolara dönüştürmek ve teslim dosyalarını hazırlamak.
- Kısa özet: KPI özeti, araştırma sorusu özeti ve segment yorumlama tablolarını üret; segment sayısı grafiğini çiz; README'yi ve prompt günlüğünü tamamla.
- Üretilen çıktı: `project_kpi_summary.csv`, `research_question_summary.csv`, `segment_interpretation.csv`, `customer_segments_count.png`, güncellenmiş `README.md`.
