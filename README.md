# 🌬️ SiKuDara
### Sistem Prediksi Kualitas Udara Berbasis Neural-Swarm Intelligence

> **IF25-40404 — Kecerdasan Komputasional**  
> Program Studi Teknik Informatika, Institut Teknologi Sumatera (ITERA)  
> Tahun Akademik 2025/2026

---

## 👥 Anggota Kelompok

| No | Nama | NIM | Tugas |
|----|------|-----|-------|
| 1  | [Ade Putri Tifani] | [123140011] | Preprocessing & EDA Data |
| 2  | [Natasya Felisita Br Ginting] | [123140017] | Implementasi PSO |
| 3  | [Louis Hutabarat] | [123140052] | Implementasi ANN & Training |
| 4  | [Martino Kelvin] | [123140165] | Implementasi Fuzzy Logic |
| 5  | [Abel] | [NIM] | Tampilan Streamlit & Integrasi |

---

## 📌 Deskripsi Proyek

**SiKuDara** (Sistem Kualitas Udara) adalah aplikasi prediksi kualitas udara berbasis metode
**Neural-Swarm Intelligence** yang menggabungkan tiga algoritma Kecerdasan Komputasional:

- 🧠 **ANN (Artificial Neural Network)** — memprediksi nilai PM2.5 dari data parameter udara
- 🐝 **PSO (Particle Swarm Optimization)** — mengoptimalkan bobot ANN secara global untuk menghindari *local minima*
- 🔵 **Fuzzy Logic** — mengubah output numerik ANN menjadi kategori yang mudah dipahami pengguna

Aplikasi ini dibangun sebagai **Tugas Besar (Pengganti UAS)** mata kuliah Kecerdasan Komputasional
dan bertujuan menyelesaikan permasalahan nyata terkait pemantauan kualitas udara.

---

## 🎯 Latar Belakang Masalah

Kualitas udara merupakan salah satu indikator penting kesehatan lingkungan. Tingginya kadar
polutan seperti PM2.5, SO2, dan NO2 dapat berdampak serius pada kesehatan manusia. Namun,
pemantauan kualitas udara secara *real-time* membutuhkan alat sensor yang mahal dan tidak
selalu tersedia di setiap lokasi.

SiKuDara hadir sebagai solusi prediksi kualitas udara berbasis data historis menggunakan
pendekatan **Sistem Hibrida Kecerdasan Komputasional**, sehingga prediksi dapat dilakukan
hanya dari parameter cuaca yang mudah diukur.

---

## 🤖 Metode yang Digunakan

### Arsitektur Sistem 3 Pilar

```
INPUT                   TAHAP 1              TAHAP 2            TAHAP 3
─────────────       ─────────────        ─────────────      ─────────────
Suhu (°C)                                
Kelembaban (%)    →   [ PSO ]        →    [ ANN ]      →   [ Fuzzy ]    →  OUTPUT
Kec. Angin            Optimasi            Prediksi          Interpretasi
Kadar SO2             bobot ANN           PM2.5 (µg/m³)     Kategori
Kadar NO2             secara global                         Kualitas Udara
```

### Justifikasi Pemilihan Metode

| Metode | Peran | Alasan Dipilih |
|--------|-------|----------------|
| **ANN** | Prediksi nilai PM2.5 | Mampu memodelkan hubungan non-linear antara variabel cuaca dan kualitas udara |
| **PSO** | Optimasi bobot ANN | Menggantikan Backpropagation untuk mencari bobot ANN terbaik secara global, menghindari *local minima* |
| **Fuzzy Logic** | Interpretasi output | Mengubah angka prediksi menjadi kategori yang mudah dipahami, mengatasi sifat *black-box* ANN |

### Kategori Output Fuzzy

| Nilai PM2.5 (µg/m³) | Kategori | Warna | Saran |
|----------------------|----------|-------|-------|
| 0 – 50 | BAIK | 🟢 Hijau | Aman untuk semua aktivitas luar ruangan |
| 51 – 100 | SEDANG | 🟡 Kuning | Kelompok sensitif sebaiknya batasi aktivitas luar |
| 101 – 150 | TIDAK SEHAT | 🟠 Oranye | Kurangi aktivitas luar ruangan |
| > 150 | BERBAHAYA | 🔴 Merah | Hindari semua aktivitas luar ruangan |

---

## 📦 Dataset

**Beijing Multi-Site Air Quality Dataset**
- **Sumber:** [UCI Machine Learning Repository](https://archive.ics.uci.edu/dataset/501/beijing+multi+site+air+quality+data)
- **Ukuran:** 400.000+ baris data
- **Format:** CSV
- **Fitur yang digunakan:** `PM2.5`, `PM10`, `SO2`, `NO2`, `TEMP`, `PRES`, `DEWP`, `WSPM`

---

## 🗂️ Struktur Direktori

```
SiKuDara/
│
├── app.py                  ← Aplikasi utama Streamlit
├── train_model.py          ← Training ANN + PSO
├── pso_optimizer.py        ← Algoritma PSO
├── fuzzy_engine.py         ← Aturan Fuzzy Logic
├── preprocessing.py        ← Pembersihan & normalisasi data
├── requirements.txt        ← Daftar library
│
├── data/
│   └── air_quality.csv     ← Dataset UCI (letakkan di sini)
│
└── model/
    └── ann_model.pkl       ← Model ANN yang sudah dilatih
```

---

## ⚙️ Instalasi & Menjalankan Aplikasi

### 1. Clone Repository
```bash
git clone https://github.com/[username]/sikudara.git
cd sikudara
```

### 2. Install Library
```bash
pip install -r requirements.txt
```

### 3. Download Dataset
Download dataset dari [UCI Repository](https://archive.ics.uci.edu/dataset/501/beijing+multi+site+air+quality+data)
dan letakkan file CSV di folder `data/`.

### 4. Training Model
```bash
python train_model.py
```

### 5. Jalankan Aplikasi
```bash
streamlit run app.py
```

Aplikasi akan otomatis terbuka di browser: `http://localhost:8501`

---

## 📋 Requirements

```
streamlit==1.32.0
scikit-learn==1.4.0
pyswarms==1.3.0
scikit-fuzzy==0.4.2
pandas==2.2.0
numpy==1.26.4
matplotlib==3.8.0
plotly==5.19.0
joblib==1.3.2
```

---

## 🖥️ Tampilan Aplikasi

### Halaman Prediksi
- Input parameter udara melalui *slider* dan *number input*
- Tombol **"Prediksi Sekarang"**
- Output berupa nilai PM2.5, kategori kualitas udara berwarna, dan saran aktivitas

### Halaman Visualisasi
- Grafik tren kualitas udara historis
- Distribusi kategori kualitas udara
- Perbandingan nilai prediksi vs aktual

### Halaman Tentang Model
- Penjelasan cara kerja ANN, PSO, dan Fuzzy Logic
- Metrik akurasi model (MAE, RMSE, R²)
- Diagram arsitektur sistem

---

## 📊 Hasil & Performa Model

| Metrik | Nilai |
|--------|-------|
| MAE (Mean Absolute Error) | *[diisi setelah training]* |
| RMSE (Root Mean Square Error) | *[diisi setelah training]* |
| R² Score | *[diisi setelah training]* |

---

## 🎥 Video Presentasi

📺 Link YouTube: [*akan diupdate*]

---

## 📚 Referensi

1. Engelbrecht, A. P. (2007). *Computational Intelligence: An Introduction*. Wiley.
2. Jang, J.-S. R. (1993). ANFIS: adaptive-network-based fuzzy inference system. *IEEE Transactions on Systems, Man, and Cybernetics*.
3. Kennedy, J., & Eberhart, R. (1995). Particle swarm optimization. *Proceedings of IEEE International Conference on Neural Networks*.
4. Zadeh, L. A. (1965). Fuzzy sets. *Information and Control*, 8(3), 338–353.
5. UCI Machine Learning Repository. *Beijing Multi-Site Air Quality Data Set*. https://archive.ics.uci.edu/dataset/501

---

## 📄 Lisensi

Proyek ini dibuat untuk keperluan akademis mata kuliah IF25-40404 Kecerdasan Komputasional,
Institut Teknologi Sumatera (ITERA) 2026.

---

<div align="center">
  <b>SiKuDara</b> — Predict the Air, Protect Your Life 🌬️<br>
  Institut Teknologi Sumatera · Teknik Informatika · 2026
</div>
