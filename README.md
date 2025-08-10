### Direnç Oranı Belirleme Programı -- Kullanım Kılavuzu 

Aşağıdaki adımlar, LabVIEW üzerinde geliştirilmiş direnç oranı hesaplama
programının doğru ve verimli bir şekilde kullanılmasını sağlar. Bu
rehber, sistemi ilk kez kullanacak kişiler için hazırlanmıştır.

#### 1. Donanım Bağlantılarının Kontrolü 

- **Dirençlerin doğru bağlandığından emin olun.**Örnek bağlantılar:

  - 1R direnç: 10 Ω

  - 10R direnç: 100 Ω

#### 2. Dekat Değerlerinin Ayarlanması 

- **Direnç dekat (yaklaştırma) değerlerini uygun şekilde ayarlayın.**

  - Kural: 1R\'nin değeri x2, 10R\'nin değeri 1/10 olacak şekilde ayarlanmalıdır.

  - Örneğin:

    - 1R = 10 Ω ise, dekat değeri = 20 Ω

    - 10R = 100 Ω ise, dekat değeri = 10 Ω

- **Gerekliyse kapasitans dekat ayarlarını da yapın.**

#### Lock-in amplifikatör yeniden başlatıldığında bazı ayarların tekrar yapılması gerekmektedir. Gerekli ayarlar aşağıda görsellerle birlikte gösterilmiştir.

**Menüde Ref Phase'a tıklıyoruz Ref. Source Internal seçilidir. Burayı "External" olarak değiştiriyoruz.**

**Menüde "Input Filters"a tıklıyoruz Line Notches Out seçilidir burayı Both yapıyoruz.**

**Menüde "GAINTC" ye tıklıyoruz burada Filter db/oct 12 olarak seçilidir burayı 24 yapıyoruz.**


#### 3. İki Farklı Çalışma Senaryosu

Programı kullanma amacınıza göre iki farklı senaryodan birini
seçebilirsiniz:

### **Senaryo 1: Hazır Veriyi Kullanarak Dengeleme**

1.  Ana program arayüzünde, **\"Frekans Seçimi\"** adlı listeden dengelemek istediğiniz frekansı seçin.

2.  Sağdaki listeden aynı frekansın üzerine çift tıklayarak ilgili Excel dosyasını yükleyin.

3.  Ardından **"Başlat"** butonuna tıklayarak işlemi başlatın.

Bu yöntem, önceden ölçülmüş ve kaydedilmiş verileri kullanarak hızlıca dengeleme yapmanızı sağlar.

### **Senaryo 2: Sıfırdan Manuel Dengeleme**

1.  **\"DB_GLOBAL_4_Kart_Test\"** programını açın.

2.  \"Frequency\" (Frekans) alanına dengeleme yapmak istediğiniz frekansı girin.

3.  **"ON/OFF" kutucuğunu işaretleyin.**(İşaretlenmediği takdirde sistem varsayılan olarak 1000 Hz\'de kalır.)

4.  Ardından **\"First Input Values\"** programına geçin:

    1.  Burada X ve Y için Input1, Input2 ve Range değerlerini belirleyin.

    2.  Bu değerleri, **Lock-In Amplifier** cihazında gözlemleyerek girin.

5.  Giriş değerlerini tamamladıktan sonra, tekrar **\"DB_GLOBAL_4_Kart_Test\"** programına dönün:

    1.  Frekans kutusundaki işareti kaldırın.

    2.  Ana programda yer alan Ana Denge 10R 1R Wagner Kelvin için dengeleme yapılacak tüm noktalar için denge koşullarını girin:

        1.  X1: Kaba ölçüm

        2.  X2: Hassas ölçüm

        3.  Y1, Y2: Aynı şekilde

Not: Her dengeleme işlemi için güvenilir (kararlı) input ve range değerleri seçilmelidir.

Kaba ölçüm değerlerini mümkün olduğunca yüksek verin.

Bu aşamada sistem, Lock-In Amplifier'da maksimum hassasiyetle (Max) çalıştığı için sinyal oynaklığı fazla olabilir.

**Kaba ölçüm sınırları:**

- Ana denge ve Kelvin: En fazla **5 µV**

- 10R, 1R, Wagner: En fazla **500 µV**

#### 4. Son Aşama 

- Tüm ayarları yaptıktan sonra programı durdurun ve tekrar başlatın.

- Ana programdan tekrar **frekans seçimini** yapın.

- Ardından **"Başlat"** butonuna basarak işlemi başlatın.

### Birden Fazla Frekans ile Ölçüm Almak 

Eğer birden fazla frekansla ölçüm yapacaksanız, kullanacağınız yöntem hazır veri kullanımına göre değişiklik gösterebilir:

#### **1. Hazır Verilerle Ölçüm (Excel Verisi Kullanarak)** 

- Bu durumda, standart işlem adımlarında **hiçbir değişiklik yoktur.**

- Sadece ana programda **"Frekans Seçimi"** listbox'ından birden fazla frekans seçin.

- Her frekans için, sağdaki listbox'tan ilgili Excel dosyasını çift tıklayarak yükleyin.

- Tüm frekansların verileri yüklendikten sonra, **"Başlat"** butonuna tıklayarak işlemi başlatabilirsiniz.

#### **2. Hazır Veri Olmadan, Manuel Olarak Ölçüm (Multi-Frekans Dengeleme)** 

Eğer elinizde hazır Excel verileri yoksa ve birden fazla frekansla ölçüm yapmak istiyorsanız, aşağıdaki adımları takip edin:

1.  **\"First Input Values\"** programını açın.

2.  Sağ tarafta yer alan **ok işaretlerini (navigasyon tuşları)** göreceksiniz. Bunlar, çoklu frekans girişlerinde sizi yönlendirecektir.

3.  **\"Active\"** butonunu **aktif hale getirin.**

4.  **MultiValues Array** bölümünde, kaç frekans için ölçüm yapacaksanız o kadar konfigürasyon oluşturmanız gerekir.

    - Örneğin, 3 frekans için ölçüm yapılacaksa, array'i \[0,0,0\] şeklinde başlatabilirsiniz.

    - Her bir array girişi, soldaki input1, input2 ve range ayarlarıyla **aynı sırada** girilmelidir.

    - Bu ilk frekans için geçerli olacaktır.

    - İkinci frekans için array'in ilk elemanını 1 yapın → \[1,0,0\]

    - Üçüncü frekans için → \[2,0,0\] şeklinde ilerleyin.

Bu şekilde her frekans için ayrı giriş değerleri tanımlanmış olur.

1.  Ardından, **Ana Program** ekranına geri dönün.

    - Sağ alt köşede yer alan tabloyu göreceksiniz (AD X_1, AD X_2 vb.).

    - Bu tablo, her frekans için ayrı ayrı girilecek **denge koşullarını** temsil eder.

    - Her bir frekans için bu denge değerlerini tabloya girin.

2.  Tüm verileri girdikten sonra:

    - Programı **durdurun** ve tekrar **başlatın.**

    - Ana programda Listbox üzerinden ölçüm yapılacak frekansları tekrar seçin.

    - Ardından **"Başlat"** butonuna basarak çoklu frekansla dengeleme işlemini başlatabilirsiniz.
