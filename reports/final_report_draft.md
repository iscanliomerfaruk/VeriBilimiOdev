# Online Retail II Veri Seti ile E-Ticaret Müşteri Davranışı Analizi

**Öğrenci:** Ömer Faruk İşcanlı — 1306220071

## 1. Problem Tanımı

Bu çalışmanın amacı, UCI Online Retail II veri seti kullanılarak e-ticaret müşteri davranışını analiz etmek ve müşterileri satın alma davranışlarına göre anlaşılır segmentlere ayırmaktır. Proje kapsamında işlem düzeyindeki veriler temizlenmiş, temel keşifsel veri analizi yapılmış, satış ve ürün performansı incelenmiş ve müşteri düzeyinde RFM özellikleri oluşturulmuştur.

Çalışma şu araştırma sorularına odaklanır:

- Toplam satışlar zaman içinde nasıl değişmektedir?
- En yüksek geliri hangi ülkeler oluşturmaktadır?
- En yüksek geliri hangi ürünler sağlamaktadır?
- Sayısal sipariş değişkenleri sipariş davranışı hakkında ne göstermektedir?
- RFM kümeleme ile hangi müşteri segmentleri bulunmaktadır?

## 2. Veri Seti ve Kaynak

Kullanılan veri seti UCI Machine Learning Repository üzerinde yayımlanan Online Retail II veri setidir. Veri setinin lisansı CC BY 4.0 olarak belirtilmiştir. Veri, e-ticaret işlem kayıtlarını içerir ve temel değişkenler arasında fatura numarası, ürün kodu, ürün açıklaması, miktar, fatura tarihi, birim fiyat, müşteri kimliği ve ülke bilgisi bulunur.

Temizlenmiş veri setinde 779.425 işlem satırı, 5.878 tekil müşteri, 36.969 tekil fatura, 4.631 tekil ürün ve 41 ülke yer almaktadır. Tarih aralığı 2009-12-01 ile 2011-12-09 arasındadır. Temizlenmiş toplam gelir 17.374.804,27 ve ortalama fatura geliri 469,98 olarak hesaplanmıştır.

## 3. Yöntem

İlk adımda ham veri projeye alınmış ve ana Jupyter not defterinde yüklenmiştir. Ardından veri yapısı incelenmiş, eksik değerler, tekrar eden satırlar, iptal faturaları, pozitif olmayan miktar ve fiyat kayıtları kontrol edilmiştir.

Temizleme aşamasında müşteri kimliği eksik olan kayıtlar, iptal faturaları, miktarı sıfır veya negatif olan kayıtlar, birim fiyatı sıfır veya negatif olan kayıtlar ve tam tekrar eden satırlar çıkarılmıştır. Ayrıca `TotalPrice` değişkeni `Quantity * UnitPrice` olarak oluşturulmuştur. Bu değişken gelir analizleri ve RFM modellemesi için temel ölçüt olarak kullanılmıştır.

Keşifsel veri analizinde aylık gelir trendi, ülkelere göre gelir, ürünlere göre gelir ve sayısal değişkenlerin dağılımı incelenmiştir. Görselleştirme olarak çizgi grafiği, çubuk grafikleri, histogram ve korelasyon ısı haritası kullanılmıştır.

Müşteri segmentasyonu için RFM yaklaşımı uygulanmıştır. Recency, müşterinin son satın almasından bu yana geçen gün sayısını; Frequency, müşterinin tekil fatura sayısını; Monetary ise müşterinin toplam harcamasını ifade eder. Bu üç özellik `log1p` dönüşümü ile çarpıklığı azaltılarak ölçeklenmiş ve StandardScaler ile standartlaştırılmıştır. Daha sonra K-Means modeli denenmiş ve yorumlanabilirlik ile metrikler birlikte değerlendirilerek dört küme seçilmiştir.

## 4. Bulgular

Toplam satışların zaman içindeki değişimi incelendiğinde, aylık gelirin en yüksek olduğu ay 2010-11 olarak bulunmuştur. Bu ayda toplam gelir 1.166.460,02 seviyesine ulaşmıştır. Bu sonuç, satışlarda dönemsel dalgalanmalar olabileceğini göstermektedir; ancak promosyonlar, tatil dönemleri veya iş bağlamı gibi dış faktörler bu analizde ayrıca doğrulanmamıştır.

Ülke bazında gelir analizi, gelirin büyük ölçüde United Kingdom üzerinde yoğunlaştığını göstermiştir. United Kingdom toplam 14.389.234,92 gelir ile en yüksek gelir üreten ülkedir. Bu bulgu, işletmenin gelir yapısında ana pazarın belirgin biçimde baskın olduğunu gösterir.

Ürün bazında gelir analizinde en yüksek gelir sağlayan ürün REGENCY CAKESTAND 3 TIER olarak bulunmuştur. Bu ürünün toplam geliri 277.656,25 olarak hesaplanmıştır. Bununla birlikte ürün açıklamalarında gürültü ve Manual gibi standart ürün olmayabilecek satırlar bulunduğu için ürün düzeyindeki yorumlar dikkatli ele alınmalıdır.

Sayısal sipariş değişkenleri, işlem satırı değerlerinin sağa çarpık olduğunu göstermektedir. `TotalPrice` ortalaması 22,29 iken medyanı 12,48'dir. Bu fark, çok sayıda küçük işlem satırı ve az sayıda yüksek değerli işlem satırı olduğunu göstermektedir.

RFM kümeleme sonucunda dört müşteri segmenti elde edilmiştir. Yüksek değerli sadık müşteriler segmentinde 1.196 müşteri vardır ve bu segment en yüksek ortalama frekans ile en yüksek ortalama parasal değere sahiptir. Güncel orta seviye müşteriler yakın zamanda alışveriş yapmış ancak daha düşük frekans ve harcama göstermiştir. Uyuyan ancak daha yüksek harcamalı müşteriler geçmişte değerli olmuş fakat güncel etkileşimi zayıflamış müşterilerden oluşur. İnaktif düşük değerli müşteriler ise 1.973 müşteriyle en büyük segmenttir ve en düşük frekans ile en düşük ortalama harcamaya sahiptir.

Bu bulgular e-ticaret işletmesi için kampanya önceliklendirme, müşteri elde tutma, yeniden aktivasyon ve ürün odağı açısından pratik bir başlangıç noktası sağlar. Özellikle yüksek değerli sadık müşterilerin korunması, güncel orta seviye müşterilerin tekrar satın almaya yönlendirilmesi ve geçmişte değerli olan müşterilere yeniden aktivasyon kampanyaları tasarlanması önerilebilir.

## 5. Sınırlamalar

Analiz yalnızca tarihsel işlem verilerine dayanmaktadır ve gelecekteki davranışı garanti etmez. K-Means kümeleme keşifsel bir yöntemdir; segmentler neden-sonuç ilişkisi kurmaz. Temizleme aşamasında iptal kayıtlarının, müşteri kimliği eksik satırların ve pozitif olmayan miktar veya fiyat kayıtlarının çıkarılması sonuçları etkileyebilir.

Ürün açıklamalarında gürültü bulunabilir ve bazı satırlar standart ürün yerine hizmet, manuel düzeltme veya işlem türü olabilir. Ayrıca analiz, müşteri edinme maliyeti, karlılık, stok durumu, kampanyalar veya dış dönemsel faktörleri içermez. Bu nedenle bulgular karar alma sürecinde bağlamsal iş bilgisiyle birlikte değerlendirilmelidir.

## 6. Öğrenilenler

Bu proje, veri bilimi sürecinde düzenli fazlara ayrılmış bir iş akışının önemini göstermiştir. Veri yükleme, temizlik, keşifsel analiz, özellik mühendisliği, modelleme ve sonuçların raporlanması ayrı adımlar olarak ele alınmıştır.

RFM yaklaşımı, işlem verisini müşteri düzeyinde anlamlı özelliklere dönüştürmek için pratik bir yöntem sunmuştur. K-Means modeli ise basit ve açıklanabilir bir segmentasyon başlangıcı sağlamıştır. Bununla birlikte model çıktılarının iş bağlamıyla birlikte yorumlanması ve keşifsel sonuçların kesin neden-sonuç ilişkisi gibi sunulmaması gerektiği görülmüştür.
