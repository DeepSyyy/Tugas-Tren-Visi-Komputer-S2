# ♻️ Recyclable and Household Waste Classification using MobileNetV2

Proyek ini bertujuan membangun model klasifikasi gambar berbasis deep learning untuk mengenali berbagai jenis sampah rumah tangga dan daur ulang. Model menggunakan **MobileNetV2** dan dilatih dengan dataset dari [Kaggle: Recyclable and Household Waste Classification](https://www.kaggle.com/datasets/alistairking/recyclable-and-household-waste-classification).

---

## 📦 Dataset Overview

- **Sumber**: [Kaggle – Alistair King](https://www.kaggle.com/datasets/alistairking/recyclable-and-household-waste-classification)
- **Total Kategori**: Beragam jenis sampah terbagi dalam beberapa kategori besar dan subkategori spesifik.
- **Format Gambar**: `.png`
- **Struktur Folder**:

  ```
  images/
  ├── Plastic water bottles/
  │   ├── default/
  │   └── real_world/
  ├── Newspaper/
  ├── Aluminum soda cans/
  ├── Food waste/
  ├── Clothing/
  └── ...
  ```

Setiap subkategori memiliki dua kondisi:

- `default`: citra studio atau kondisi terkendali
- `real_world`: citra di lingkungan nyata (sampah di jalan, dapur, dll)

Contoh dataset yang digunakan:

---

## 🧠 Model & Pipeline

### 1. **Preprocessing**

- Resize gambar ke `224x224`
- Augmentasi: flip, rotation, zoom, dll
- Normalisasi menggunakan `preprocess_input` dari MobileNetV2

### 2. **Modeling**

- Backbone: **MobileNetV2** pretrained (imagenet)
- Custom classifier head dengan dense layers dan dropout
- Transfer learning: freezing sebagian besar layer MobileNetV2
- Fine-tuning pada layer akhir

### 3. **Training**

- Optimizer: Adam
- Loss: categorical crossentropy
- Early stopping & model checkpoint
- Evaluasi pada test set: akurasi, classification report, confusion matrix

### 4. **Inference**

- Uji model pada gambar individual
- Visualisasi hasil prediksi

---

## 📊 Hasil

- Akurasi tinggi tercapai pada data `default`
- Akurasi menurun pada `real_world` karena noise lingkungan, menunjukkan tantangan dunia nyata
- Fine-tuning model memberi peningkatan performa pada data real-world

---

📈 Evaluasi

Berikut visualisasi performa model:

Akurasi & Loss

Gambar di atas menunjukkan kurva akurasi dan loss selama pelatihan:

Akurasi validasi stabil mendekati 85%

Tidak terdapat overfitting yang signifikan

Confusion Matrix

Confusion matrix memperlihatkan distribusi prediksi model terhadap masing-masing kelas. Model menunjukkan performa yang konsisten pada sebagian besar kategori, namun masih terdapat kebingungan pada beberapa kelas yang serupa (misal: aluminum_food_cans vs steel_food_cans).

---

## 🚀 Menjalankan Proyek

1. Clone repo:

   ```bash
   git clone https://github.com/username/repo-name.git
   cd repo-name
   ```

2. Install dependencies:

   ```bash
   pip install -r requirements.txt
   ```

3. Jalankan notebook:
   ```bash
   jupyter notebook Final_Tren_Viskom.ipynb
   ```

---

## 👤 Kontributor

- Falah Asyraf Darmawan Putra
- Akif Rachmat Hidayah

---

## 📄 Lisensi & Penggunaan

Dataset ini dapat digunakan untuk keperluan edukasi dan riset. Mohon sertakan atribusi berikut jika menggunakan dataset:

> Alistair King, www.kaggle.com/datasets/alistairking/recyclable-and-household-waste-classification

---

## 🌱 Harapan

Semoga proyek ini berkontribusi pada peningkatan kesadaran dan teknologi dalam pengelolaan sampah untuk lingkungan yang lebih bersih dan berkelanjutan.
