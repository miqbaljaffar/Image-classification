# Klasifikasi Jenis Kendaraan menggunakan Convolutional Neural Network (CNN) 🚗✈️🚢🚆🏍️

## 📌 Ringkasan Proyek

Proyek ini bertujuan untuk membangun model *deep learning* yang mampu mengklasifikasikan berbagai jenis kendaraan. Model dilatih untuk mengenali tujuh kategori kendaraan, yaitu:

* **Auto Rickshaws**
* **Bikes**
* **Cars**
* **Motorcycles**
* **Planes**
* **Ships**
* **Trains**

---

## 📊 Dataset

Dataset yang digunakan dalam proyek ini berasal dari Kaggle:

* **Sumber**: [Vehicle Classification Dataset](https://www.kaggle.com/datasets/mohamedmaher5/vehicle-classification)
* **Detail**: Setiap kategori memiliki sekitar **800 gambar**, menjadikannya dataset yang cukup seimbang untuk pelatihan model.

---

## ⚙️ Metodologi

### 1. Persiapan Data

* **Pengambilan Data**: Mengunduh dataset dari Kaggle.
* **Pemisahan Data**: Dataset dibagi menjadi:

  * Data latih: 70%
  * Data validasi: 15%
  * Data uji: 15%
* **Normalisasi**: Nilai piksel dinormalisasi ke rentang \[0, 1].
* **Augmentasi Data**: Untuk mengurangi *overfitting*, dilakukan augmentasi seperti:

  * Rotasi
  * Pergeseran lebar dan tinggi
  * *Shear*
  * Zoom
  * *Horizontal flip*
  * Penyesuaian kecerahan

### 2. Pengembangan Model

* **Arsitektur**: Menggunakan arsitektur **CNN kustom** tanpa *transfer learning*, terdiri dari:

  * Lapisan konvolusi
  * *Batch normalization*
  * Aktivasi ReLU
  * *Max pooling*
  * *Fully connected layers* dengan *dropout*
* **Callbacks**:

  * `ModelCheckpoint`: Simpan bobot terbaik.
  * `EarlyStopping`: Menghentikan pelatihan saat validasi stagnan.
  * `ReduceLROnPlateau`: Turunkan *learning rate* jika *validation loss* tidak membaik.

### 3. Pelatihan dan Evaluasi

* Model dilatih dengan data latih dan dievaluasi terhadap data validasi pada setiap *epoch*.
* Setelah pelatihan, model terbaik diuji menggunakan data uji.

---

## 📈 Hasil Evaluasi

| Metode Evaluasi          | Nilai      |
| ------------------------ | ---------- |
| Akurasi Data Uji         | **93.39%** |
| Loss Data Uji            | **0.3890** |
| Akurasi Akhir Data Latih | 84.38%     |
| Akurasi Akhir Validasi   | 92.07%     |

> Hasil ini menunjukkan bahwa model mampu melakukan generalisasi dengan baik terhadap data yang belum pernah dilihat sebelumnya.

---

## 💾 Penyimpanan dan Konversi Model

Model disimpan dalam berbagai format untuk keperluan deployment:

1. **TensorFlow SavedModel**
   Format standar untuk deployment di lingkungan TensorFlow.

2. **TensorFlow Lite (`.tflite`)**
   Optimasi untuk perangkat mobile dan *edge*, disertai file `label.txt`.

3. **TensorFlow\.js (`tfjs_model`)**
   Format untuk dijalankan di browser/web menggunakan JavaScript.

---

## 🚀 Inferensi

Dilakukan uji inferensi untuk memvalidasi bahwa model dapat memprediksi kelas dari gambar kendaraan secara acak dari data uji. Ini menunjukkan bahwa model siap digunakan untuk prediksi aktual.

---

## 📂 Struktur Folder Proyek

```
submission/
├── tfjs_model/
│   ├── group1-shard1of1.bin
│   └── model.json
├── tflite/
│   ├── model.tflite
│   └── label.txt
├── saved_model/
│   ├── saved_model.pb
│   └── variables/
├── notebook.ipynb
├── README.md
└── requirements.txt
```

---

## 🔄 Cara Menjalankan Kembali (Reproduksi)

1. Pastikan environment Python kamu memiliki library berikut:

   * `TensorFlow`
   * `Matplotlib`
   * `split-folders`
   * dan library lainnya yang tercantum di `requirements.txt`

2. Unduh dataset dari Kaggle sesuai link yang diberikan.

3. Jalankan notebook `notebook.ipynb` untuk memulai pelatihan ulang.

4. Hasil model akan otomatis tersimpan dalam folder `submission/`.

---