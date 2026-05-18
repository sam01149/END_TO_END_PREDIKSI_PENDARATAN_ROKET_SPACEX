# End-to-End Prediksi Pendaratan Roket SpaceX Falcon 9

Proyek data science end-to-end untuk memprediksi keberhasilan pendaratan tahap pertama roket **SpaceX Falcon 9** menggunakan machine learning — mencakup pengumpulan data dari API, eksplorasi, visualisasi geospasial, hingga deployment model klasifikasi.

---

## Latar Belakang

SpaceX berhasil menekan biaya peluncuran roket dari **$165 juta** menjadi **$62 juta** dengan mendaur ulang tahap pertama (first stage booster) Falcon 9. Kunci penghematan ini adalah keberhasilan pendaratan booster setelah peluncuran.

> **Pertanyaan utama:** Dapatkah kita memprediksi apakah tahap pertama Falcon 9 akan berhasil mendarat, berdasarkan parameter misi?

---

## Alur Proyek

```
1. Data Collection       → SpaceX REST API
        ↓
2. Data Wrangling        → Pembersihan & encoding label
        ↓
3. Exploratory Data Analysis (EDA)
        ↓
4. SQL Analysis          → Query berbasis database
        ↓
5. Geospatial Visualization → Folium interactive map
        ↓
6. Machine Learning      → Klasifikasi biner (berhasil/gagal)
```

---

## Struktur Notebook

| File | Deskripsi |
|---|---|
| `Data_Collection.ipynb` | Pengambilan data historis Falcon 9 via SpaceX REST API |
| `spacex_data_wrangling.ipynb` | Pembersihan data & pembuatan kolom target `Class` |
| `Exploratory Data Analysis.ipynb` | Eksplorasi fitur dan distribusi data |
| `Exploratory_Using_sql.ipynb` | Analisis data menggunakan query SQL |
| `Spacex_Vizualization.ipynb` | Peta interaktif lokasi peluncuran dan outcome |
| `Spacex_Machinelearning.ipynb` | Pemodelan ML dan evaluasi model |

---

## Dataset

**Sumber:** SpaceX REST API (`api.spacexdata.com/v4/`)

Endpoint yang digunakan:
- `/launches/past` — rekaman peluncuran historis
- `/rockets/` — informasi versi booster
- `/launchpads/` — detail lokasi peluncuran
- `/payloads/` — spesifikasi muatan
- `/cores/` — data performa tahap pertama

**Ukuran dataset:** 90 baris × 18 kolom

**Target variable:** `Class`
- `1` = Pendaratan berhasil (True ASDS / True RTLS / True Ocean)
- `0` = Pendaratan gagal

**Tingkat keberhasilan historis:** ~66.67%

### Fitur Utama

| Kategori | Fitur |
|---|---|
| Metadata misi | `FlightNumber`, `Date`, `BoosterVersion` |
| Parameter misi | `PayloadMass`, `Orbit`, `LaunchSite` |
| Detail booster | `GridFins`, `Reused`, `Legs`, `Block`, `ReusedCount`, `Serial` |
| Lokasi | `Longitude`, `Latitude`, `LandingPad` |

---

## Lokasi Peluncuran

Empat fasilitas peluncuran SpaceX yang dianalisis:

| Lokasi | Kode |
|---|---|
| Cape Canaveral | CCAFS LC-40 |
| Cape Canaveral | CCAFS SLC-40 |
| Kennedy Space Center | KSC LC-39A |
| Vandenberg | VAFB SLC-4E |

Semua lokasi berada di tepi pantai — strategis untuk keselamatan dan logistik peluncuran.

---

## Hasil Machine Learning

### Model yang Dievaluasi

| Model | Akurasi |
|---|---|
| Logistic Regression | 84.64% |
| **Support Vector Machine (SVM)** | **84.82%** ← Terbaik |
| Decision Tree | — |

### Model Terbaik: **SVM**

```
Kernel  : sigmoid
C       : 1.0
Gamma   : 0.0316
```

**Jumlah fitur setelah preprocessing:** 83 fitur (one-hot encoding + normalisasi)

---

## Teknologi

- **Python 3.x**
- `pandas`, `numpy` — manipulasi data
- `matplotlib`, `seaborn` — visualisasi statis
- `folium` — peta interaktif geospasial
- `scikit-learn` — preprocessing & machine learning
- `sqlite3` / `sqlalchemy` — analisis SQL

---

## Cara Menjalankan

1. Clone repository ini:
   ```bash
   git clone https://github.com/sam01149/END_TO_END_PREDIKSI_PENDARATAN_ROKET_SPACEX.git
   cd END_TO_END_PREDIKSI_PENDARATAN_ROKET_SPACEX
   ```

2. Install dependencies:
   ```bash
   pip install pandas numpy matplotlib seaborn scikit-learn folium requests sqlalchemy
   ```

3. Jalankan notebook secara berurutan:
   ```
   1. Data_Collection.ipynb
   2. spacex_data_wrangling.ipynb
   3. Exploratory Data Analysis.ipynb
   4. Exploratory_Using_sql.ipynb
   5. Spacex_Vizualization.ipynb
   6. Spacex_Machinelearning.ipynb
   ```

---

## Kesimpulan

- Model SVM berhasil memprediksi keberhasilan pendaratan Falcon 9 dengan akurasi **~85%**
- Fitur seperti orbit, payload mass, lokasi peluncuran, dan status reuse booster berpengaruh signifikan terhadap keberhasilan pendaratan
- Analisis geospasial menunjukkan semua lokasi peluncuran SpaceX berada di tepi pantai dengan pola keberhasilan yang bervariasi antar lokasi

---

## Author

**Samuel** — Data Science Capstone Project
