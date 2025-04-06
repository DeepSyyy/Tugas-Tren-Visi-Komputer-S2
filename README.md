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

![Contoh Gambar Dataset](https://github.com/DeepSyyy/Tugas-Tren-Visi-Komputer-S2/blob/main/images/example-of-datasets.png?raw=true)

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

---

## 📊 Hasil

- Akurasi tinggi tercapai pada data `default`
- Akurasi menurun pada `real_world` karena noise lingkungan, menunjukkan tantangan dunia nyata
- Fine-tuning model memberi peningkatan performa pada data real-world

---

## 📈 Evaluasi

Berikut visualisasi performa model:

![Akurasi dan Loss](https://github.com/DeepSyyy/Tugas-Tren-Visi-Komputer-S2/blob/main/images/train-val-model-recycle.png?raw=true)

Gambar di atas menunjukkan kurva akurasi dan loss selama pelatihan:

- Akurasi validasi stabil mendekati 85%

- Tidak terdapat overfitting yang signifikan

![Confussion Matrix](https://github.com/DeepSyyy/Tugas-Tren-Visi-Komputer-S2/blob/main/images/confussion-matrix-recycle.png?raw=true)

Confusion matrix memperlihatkan distribusi prediksi model terhadap masing-masing kelas. Model menunjukkan performa yang konsisten pada sebagian besar kategori, namun masih terdapat kebingungan pada beberapa kelas yang serupa (misal: aluminum_food_cans vs steel_food_cans).

## Classification Report


| Label                         | Precision | Recall | F1-Score | Support |
|------------------------------|-----------|--------|----------|---------|
| aerosol_cans                 | 0.93      | 0.82   | 0.87     | 45      |
| aluminum_food_cans          | 0.72      | 0.55   | 0.63     | 47      |
| aluminum_soda_cans          | 0.76      | 0.82   | 0.79     | 45      |
| cardboard_boxes             | 0.62      | 0.60   | 0.61     | 47      |
| cardboard_packaging         | 0.61      | 0.65   | 0.63     | 48      |
| clothing                    | 0.84      | 0.96   | 0.90     | 45      |
| coffee_grounds              | 1.00      | 1.00   | 1.00     | 47      |
| disposable_plastic_cutlery  | 0.96      | 0.90   | 0.93     | 49      |
| eggshells                   | 0.87      | 0.98   | 0.92     | 48      |
| food_waste                  | 0.85      | 0.85   | 0.85     | 48      |
| glass_beverage_bottles      | 0.89      | 0.88   | 0.88     | 48      |
| glass_cosmetic_containers   | 0.98      | 0.86   | 0.91     | 49      |
| glass_food_jars             | 0.86      | 0.88   | 0.87     | 49      |
| magazines                   | 0.92      | 0.94   | 0.93     | 48      |
| newspaper                   | 0.74      | 0.86   | 0.80     | 43      |
| office_paper                | 0.80      | 0.77   | 0.78     | 47      |
| paper_cups                  | 0.88      | 0.75   | 0.81     | 48      |
| plastic_cup_lids            | 0.79      | 0.90   | 0.84     | 49      |
| plastic_detergent_bottles   | 1.00      | 0.96   | 0.98     | 47      |
| plastic_food_containers     | 0.93      | 0.91   | 0.92     | 45      |
| plastic_shopping_bags       | 0.78      | 0.83   | 0.80     | 47      |
| plastic_soda_bottles        | 0.81      | 0.90   | 0.85     | 49      |
| plastic_straws              | 0.91      | 0.85   | 0.88     | 48      |
| plastic_trash_bags          | 0.89      | 0.86   | 0.88     | 49      |
| plastic_water_bottles       | 0.79      | 0.81   | 0.80     | 47      |
| shoes                       | 0.98      | 0.86   | 0.91     | 49      |
| steel_food_cans             | 0.69      | 0.77   | 0.73     | 48      |
| styrofoam_cups              | 0.89      | 0.88   | 0.88     | 48      |
| styrofoam_food_containers   | 0.93      | 0.86   | 0.89     | 49      |
| tea_bags                    | 0.83      | 0.94   | 0.88     | 47      |
| Accuracy                    |           |        | 0.85     | 1423    |
| Macro avg                   | 0.85      | 0.85   | 0.84     | 1423    |
| Weighted avg                | 0.85      | 0.85   | 0.85     | 1423    |


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
