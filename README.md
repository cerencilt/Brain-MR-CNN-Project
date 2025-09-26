# Brain MRI Tümör Tespiti – CNN & Transfer Learning

Bu repo, **Global AI Hub Bootcamp** kapsamında geliştirilen **beyin MRI görüntülerinden tümör tespiti** projesini içermektedir.  
Proje; temel bir **Convolutional Neural Network (CNN)** modeli ile **VGG16 tabanlı Transfer Learning** yaklaşımını karşılaştırmalı olarak ele almaktadır.

---

## Giriş

- **Veri Seti:**  
  - **Kaynak:** https://www.kaggle.com/datasets/preetviradiya/brian-tumor-dataset  
  - **Klasör Yapısı:** `/kaggle/input/brian-tumor-dataset/Brain Tumor Data Set/Brain Tumor Data Set/`  
  - **Toplam Görüntü:** 4,600  
    - Brain Tumor: 2,513  
    - Healthy: 2,087  
- **Amaç:** Beyin MR görüntülerini “Brain Tumor” ve “Healthy” olarak **iki sınıfta** sınıflandırmak.

### Veri Ön İşleme
- Görseller **grayscale** formatına çevrildi ve **128×128** piksel boyutuna yeniden boyutlandırıldı.
- Piksel değerleri **0–1 aralığına normalize** edildi.
- Etiketler **one-hot encoding** ile iki sınıf için [4600, 2] boyutuna dönüştürüldü.
- **ImageDataGenerator** ile veri artırma (augmentation) uygulandı:
  - Küçük açısal dönüşler, yatay/dikey kaydırmalar, yatay çevirme, yakınlaştırma.

---

## Kullanılan Teknolojiler
- **Python 3.x**
- **TensorFlow / Keras**
- NumPy, Pandas, Matplotlib, scikit-learn
- (Opsiyonel) Google Colab / Kaggle Notebook

---

## Model Mimarileri

### Temel CNN Modeli
- **3 Konvolüsyon Bloğu:** 32 → 64 → 128 filtre  
- Her blokta **Batch Normalization, MaxPooling, Dropout**
- **Flatten + Dense** katmanları ve Softmax çıkış
- **Toplam Parametre:** 4,482,530 (4,481,826 trainable)
- **Optimizasyon:**  
  - *Early Stopping* (10 epoch sabır)  
  - *ReduceLROnPlateau* (iyileşme yoksa learning rate %80 azaltılır)

### Transfer Learning Modeli (VGG16)
- **Ön İşleme:** Grayscale görüntüler 3 kanala çoğaltıldı → (128, 128, 3)
- **Önceden Eğitilmiş Katmanlar:** `trainable=False`
- **Ek Katmanlar:**  
  - GlobalAveragePooling2D  
  - Dense(256) + Dropout(0.5)  
  - Dense(2, activation="softmax")

---

## Metrikler

| Model                 | Test Doğruluğu | Precision | Recall | F1-Score |
|-----------------------|---------------|----------|-------|--------|
| **Temel CNN**         | **0.98**      | 0.98     | 0.98  | 0.98   |
| **Transfer Learning** | **0.9283**    | –        | –     | –     |

**CNN Sınıflandırma Raporu:**  
- Brain Tumor – Precision: 0.98, Recall: 0.98  
- Healthy – Precision: 0.98, Recall: 0.97  
- Macro Avg F1: 0.98


---

## Sonuç ve Değerlendirme

- **Temel CNN**, %98 test doğruluğu ile veri seti için en yüksek performansı göstermiştir.
- **Transfer Learning (VGG16)**, %89 doğruluk ile güçlü bir alternatif sunmuş, ancak bu veri seti özelinde CNN’in gerisinde kalmıştır.
- Yanlış sınıflandırma oranı oldukça düşüktür (yalnızca 20 örnek).
- Veri dengesi (2513/2087) ve data augmentation, modelin **overfitting** yapmadan genelleme yeteneğini güçlendirmiştir.

---

## Ekler (Opsiyonel Çalışmalar)

- **Aktivasyon Haritaları:** İlk 4 evrişim katmanının çıktılarını görselleştirerek modelin hangi özellikleri yakaladığını inceledik.
- **Bar Grafiği ile Karşılaştırma:** Temel CNN ve Transfer Learning modellerinin test doğrulukları görsel olarak karşılaştırılmıştır.

---

## Sonuç ve Gelecek Çalışmalar

Bu proje, beyin MR görüntülerinden tümör tespiti için yüksek doğruluklu bir temel CNN modeli sunmaktadır.  
Gelecek adımlar:
- Daha büyük ve çeşitlendirilmiş MRI veri setleriyle yeniden eğitim
- **Explainable AI (XAI)** ile model karar mekanizmalarının açıklanması
- Gerçek zamanlı tespit için **Streamlit veya Flask** tabanlı bir web arayüzü
- Mobil cihazlara entegrasyon için TensorFlow Lite dönüştürmesi

---

## 🔗 Linkler

- **Kaggle Notebook:** https://www.kaggle.com/code/cerencilt/brain-mr-project 
 

## 👩‍💻 Yazar

- **Ceren CİLT** – Global AI Hub Bootcamp Katılımcısı  
  https://github.com/cerencilt
  www.linkedin.com/in/ceren-cilt-453808246










