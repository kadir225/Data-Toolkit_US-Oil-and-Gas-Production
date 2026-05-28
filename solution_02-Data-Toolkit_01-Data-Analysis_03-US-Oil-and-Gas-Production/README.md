ABD Petrol ve Gaz Üretimi Analizi

Bu projede, Haziran 2008 – Haziran 2018 dönemine ait ABD doğal gaz ve ham petrol üretim verilerini analiz ederek kapsamlı bir zaman serisi ve agregasyon çalışması gerçekleştirdim. Proje boyunca Kaggle'dan aldığım ham verileri temizledim ve anlamlı grafiklere dönüştürdüm. Dataset[available on Kaggle](https://www.kaggle.com/djzurawski/us-oil-and-gas-production-june-2008-to-june-2018)

ABD Petrol ve Gaz Üretimi Analizi
Bu projede, Haziran 2008 – Haziran 2018 dönemine ait ABD doğal gaz ve ham petrol üretim verilerini analiz ederek kapsamlı bir zaman serisi ve agregasyon çalışması gerçekleştirdim. Proje boyunca Kaggle'dan aldığım ham verileri temizledim, manipüle ettim ve anlamlı grafiklere dönüştürdüm.

🔍 Gerçekleştirdiğim Analiz Adımları
1. Proje Ortamının Hazırlanması ve Veri Yükleme
Terminal üzerinden mkdir data komutunu kullanarak projeme özel bir veri klasörü oluşturdum ve Kaggle'dan indirdiğim veri setlerini bu dizine aldım.

Veri keşif ve analiz sürecini tamamen Jupyter Notebook (oil_and_gas.ipynb) üzerinde yürüttüm.

Projeme başlık ve açıklama içeren Markdown dokümantasyonunu ekledikten sonra, analizde sıkça kullandığım numpy, pandas ve matplotlib kütüphanelerini import ettim.

2. Doğal Gaz Verilerinin Temizlenmesi ve Datetime Dönüşümü
U.S._natural_gas_production.csv dosyasını pd.read_csv() fonksiyonuyla yükledim. shape, columns ve info() metotlarını kullanarak veri yapısını incelediğimde, Month sütununun tarih yerine object (metin) olarak tanındığını fark ettim.

Bu problemi çözmek için pd.to_datetime() fonksiyonunu kullanarak Month sütununu gerçek bir datetime nesnesine dönüştürdüm. Yazdığım bu dönüşüm kodunu nbresult test aracıyla kontrol ettim ve %100 başarı sağladım.

3. Yıllık Agregasyon ve Boolean Indexing ile Filtreleme
Eyaletlerin ve ABD genelinin yıllık toplam gaz üretimini hesaplamak adına veriyi yıl bazında grupladım (groupby). Gruplama esnasında tarih sütunlarının hata vermemesi için yalnızca sayısal sütunları toplayarak yearly_gas_df DataFrame'ini elde ettim ve full_gas testini başarıyla geçtim.

Elde ettiğim yıllık veriyi incelediğimde, 2008 ve 2018 yıllarının eksik aylara (yalnızca 6 aylık veri) sahip olduğunu gördüm. Analizin doğruluğu adına np.logical_and ve boolean indexing yöntemlerini kullanarak yalnızca tam 12 aylık verisi bulunan yılları filtreledim ve filtered_yearly_gas_df yapısını oluşturdum.

Filtrelenmiş veri üzerinden ABD toplam gaz üretimini gösteren ilk bar grafiğimi ürettim.

4. Ham Petrol Verilerinin Entegrasyonu ve Sütun Temizliği
U.S._crude_oil_production.csv dosyasını yüklerken, Pandas'ın parametrelerini kullanarak Month sütununu daha yükleme aşamasında datetime tipine dönüştürerek süreci optimize ettim.

Petrol verilerini de yıl bazında gruplayarak yearly_oil_df DataFrame'ini oluşturdum. Sütun isimlerini kontrol ettiğimde veri kalitesini bozan gizli boşluklar fark ettim ve str.strip yöntemiyle tüm sütun isimlerini temizledim.

Gaz verisinde yaptığım gibi petrol verisinde de sadece tam yılları filtreleyerek filtered_yearly_oil_df nesnesini oluşturdum ve oil testinden %100 başarı aldım.

5. Veri Setlerinin Birleştirilmesi ve Karşılaştırmalı Görselleştirme
Hem petrol hem de gaz verilerinden sadece ABD toplam üretim sütunlarını seçerek total_gas ve total_oil adında iki yeni yapı oluşturdum. Sütun isimlerini daha anlaşılır olması için Gas ve Crude Oil olarak yeniden adlandırdım.

Bu iki farklı DataFrame'i pd.concat(axis=1) fonksiyonuyla yan yana birleştirerek merged_df adında tek bir ana veri seti haline getirdim.

Son aşamada merged_dataframes testini de hatasız geçerek, iki farklı üretim türünü ve birimini (Milyon kübik fit gaz / Bin varil ham petrol) net bir şekilde gösteren, legend düzenlemeleri yapılmış karşılaştırmalı bir bar grafiği ürettim.
