# 🔄 Customer Churn Analysis
### Predictive Analytics | E-Commerce Domain

![Python](https://img.shields.io/badge/Python-3.x-3776AB?style=flat&logo=python&logoColor=white)
![Scikit-learn](https://img.shields.io/badge/Scikit--learn-ML-F7931E?style=flat&logo=scikit-learn&logoColor=white)
![Pandas](https://img.shields.io/badge/Pandas-Data-150458?style=flat&logo=pandas&logoColor=white)
![Jupyter](https://img.shields.io/badge/Jupyter-Notebook-F37626?style=flat&logo=jupyter&logoColor=white)

> **Portfolio Project #9 dari 10** — Membangun model prediktif untuk mengidentifikasi pelanggan e-commerce yang berisiko churn, sehingga tim bisnis dapat mengambil tindakan retensi yang tepat dan tepat waktu.

---

## 📋 Daftar Isi
- [Tentang Project](#-tentang-project)
- [Dataset](#-dataset)
- [Metodologi](#-metodologi)
- [Hasil Model](#-hasil-model)
- [Business Insights](#-business-insights)
- [Rekomendasi Bisnis](#-rekomendasi-bisnis)
- [Tools & Teknologi](#-tools--teknologi)
- [Struktur Project](#-struktur-project)
- [Cara Menjalankan](#-cara-menjalankan)
- [Kesimpulan](#-kesimpulan)

---

## 🎯 Tentang Project

**Churn** adalah kondisi ketika pelanggan berhenti menggunakan layanan atau berbelanja di platform. Ini adalah salah satu masalah terbesar dalam bisnis e-commerce karena:

- 💸 Biaya akuisisi pelanggan baru **5x lebih mahal** dibanding mempertahankan pelanggan lama
- 📉 Kehilangan pelanggan loyal berdampak langsung pada **revenue jangka panjang**
- 🎯 Prediksi churn yang akurat memungkinkan **strategi retensi yang efisien dan tepat waktu**

Project ini membangun model Machine Learning yang mampu memprediksi pelanggan mana yang akan churn **sebelum mereka benar-benar pergi**.

---

## 📊 Dataset

**Sumber:** [E-Commerce Customer Churn Dataset — Kaggle (Ankitverma2010)](https://www.kaggle.com/datasets/ankitverma2010/ecommerce-customer-churn-analysis-and-prediction)

| Keterangan | Detail |
|---|---|
| Total Baris | 5.630 pelanggan |
| Total Kolom | 20 fitur |
| Target Variable | `Churn` (0 = Tidak Churn, 1 = Churn) |
| Churn Rate | **16.8%** (948 pelanggan) |
| Missing Values | 7 kolom (4.4% – 5.5% per kolom) |

### Fitur Utama

| Kolom | Deskripsi | Tipe |
|---|---|---|
| `Tenure` | Lama berlangganan (bulan) | Float |
| `CashbackAmount` | Total cashback yang diterima | Float |
| `Complain` | Pernah komplain? (0/1) | Integer |
| `SatisfactionScore` | Skor kepuasan (1–5) | Integer |
| `DaySinceLastOrder` | Hari sejak order terakhir | Float |
| `WarehouseToHome` | Jarak gudang ke rumah (km) | Float |
| `OrderCount` | Jumlah order | Float |
| `PreferredPaymentMode` | Metode pembayaran favorit | String |
| `PreferedOrderCat` | Kategori order favorit | String |

---

## 🔧 Metodologi

```
📥 Load Data → 🔍 EDA → 🧹 Data Cleaning → ⚙️ Feature Engineering → 🤖 Modeling → 📈 Evaluation → 💡 Business Insights
```

### Pipeline Detail

| Tahapan | Deskripsi |
|---|---|
| **1. Data Loading** | Load dataset Excel (sheet: `E Comm`) |
| **2. EDA** | Analisis distribusi, missing values, korelasi |
| **3. Data Cleaning** | Isi missing values dengan median, hapus `CustomerID` |
| **4. Feature Engineering** | Label Encoding, perbaiki data inconsistency |
| **5. Modeling** | Train Logistic Regression & Random Forest |
| **6. Evaluation** | Confusion Matrix, ROC-AUC, Classification Report |
| **7. Business Insights** | Analisis faktor churn & rekomendasi strategis |

### Data Cleaning yang Dilakukan
- ✅ Missing values diisi dengan **median** (robust terhadap outlier)
- ✅ `CustomerID` dihapus (tidak relevan untuk prediksi)
- ✅ Perbaikan data inconsistency:
  - `'Phone'` → `'Mobile Phone'`
  - `'COD'` → `'Cash on Delivery'`
  - `'CC'` → `'Credit Card'`

### Feature Engineering
- Label Encoding pada 5 kolom kategorikal
- StandardScaler untuk normalisasi fitur (Logistic Regression)
- Train-Test Split: **80% train / 20% test** dengan `stratify=y`
- `class_weight='balanced'` untuk menangani class imbalance

---

## 🏆 Hasil Model

### Perbandingan Model

| Model | Accuracy | Precision (Churn) | Recall (Churn) | ROC-AUC |
|---|---|---|---|---|
| Logistic Regression | 77% | 41% | 81% | 0.856 |
| **Random Forest** ✅ | **98%** | **98%** | **92%** | **0.999** |

> **Model terpilih: Random Forest** — Performa terbaik di semua metrik

### Confusion Matrix — Random Forest

```
                  Prediksi: Tidak Churn   Prediksi: Churn
Aktual: Tidak Churn       933 ✅               3 ❌
Aktual: Churn              15 ❌             175 ✅
```

- ✅ **175** pelanggan churn berhasil terdeteksi
- ✅ Hanya **15** pelanggan churn yang terlewat (False Negative)
- ✅ Hanya **3** alarm palsu (False Positive)

### Feature Importance (Random Forest)

| Rank | Fitur | Importance | Interpretasi |
|---|---|---|---|
| 🥇 1 | `Tenure` | 27.35% | Paling dominan |
| 🥈 2 | `CashbackAmount` | 11.10% | Sangat berpengaruh |
| 🥉 3 | `WarehouseToHome` | 6.72% | Berpengaruh |
| 4 | `Complain` | 6.49% | Signal kuat churn |
| 5 | `DaySinceLastOrder` | 5.94% | Indikator keaktifan |
| 6 | `NumberOfAddress` | 5.61% | Berpengaruh sedang |
| 7 | `OrderAmountHike` | 5.21% | Berpengaruh sedang |
| 8 | `SatisfactionScore` | 5.07% | Berpengaruh sedang |

---

## 💡 Business Insights

### 1️⃣ Churn Rate by Tenure Group

| Tenure Group | Churn Rate | Status |
|---|---|---|
| 0–6 bulan | **25.9%** | 🔴 KRITIS — 1 dari 4 pelanggan baru pergi |
| 6–12 bulan | 9.8% | 🟡 Risiko menurun |
| 12–24 bulan | 6.5% | 🟢 Mulai loyal |
| >24 bulan | **0.0%** | 🟢 Sangat loyal, tidak ada yang churn |

### 2️⃣ Churn Rate by Satisfaction Score

| Score | Churn Rate | Catatan |
|---|---|---|
| 1 (Terendah) | 11.5% | — |
| 2 | 12.6% | — |
| 3 | 17.2% | Di atas rata-rata |
| 4 | 17.1% | Di atas rata-rata |
| 5 (Tertinggi) | ~25% | ⚠️ Counter-intuitive! |

> **Insight menarik:** Pelanggan dengan satisfaction score 5 justru paling banyak churn — menunjukkan bahwa **kepuasan saja tidak cukup** untuk retensi; ada faktor lain seperti harga kompetitor.

### 3️⃣ Churn Rate: Komplain vs Tidak

| Status Komplain | Churn Rate | Perbandingan |
|---|---|---|
| Tidak Pernah Komplain | 10.9% | Baseline |
| Pernah Komplain | **31.7%** | ⚠️ **3x lebih tinggi!** |

### 4️⃣ Cashback & Churn

| Segmen | Rata-rata Cashback |
|---|---|
| Tidak Churn | **180.6** |
| Churn | 160.4 |

> Pelanggan loyal mendapat cashback **11% lebih tinggi** — program cashback terbukti efektif untuk retensi.

---

## 📌 Rekomendasi Bisnis

### 1. 🎁 Program Welcome Loyalty (0–6 Bulan Pertama)
- **Target:** Pelanggan dengan Tenure 0–6 bulan (churn rate 25.9%)
- **Aksi:** Cashback ekstra, promo eksklusif, onboarding yang lebih personal
- **KPI:** Kurangi churn rate segmen ini di bawah 15%

### 2. 🚨 Urgent Retention untuk Pelanggan yang Komplain
- **Target:** Semua pelanggan yang baru mengajukan komplain
- **Aksi:** Follow-up dalam **24 jam**, kompensasi langsung, monitoring 30 hari
- **KPI:** Kurangi churn rate post-complaint dari 31.7% → di bawah 20%

### 3. 💰 Optimasi Program Cashback
- **Temuan:** Pelanggan churn mendapat cashback rata-rata lebih rendah (160.4 vs 180.6)
- **Aksi:** Tingkatkan cashback untuk pelanggan berisiko tinggi (hasil prediksi model)
- **KPI:** Pastikan semua pelanggan berisiko mendapat cashback minimal 175

### 4. 📱 Re-engagement Campaign untuk Pelanggan Tidak Aktif
- **Target:** Pelanggan dengan `DaySinceLastOrder` > 10 hari
- **Aksi:** Push notification & email marketing dengan penawaran personal
- **KPI:** Kurangi rata-rata hari tidak order di bawah 5 hari

### 5. 🤖 Deploy Model Prediksi Real-Time
- **Model:** Random Forest (ROC-AUC: 0.999) sudah siap di-deploy
- **Aksi:** Integrasikan dengan CRM untuk scoring otomatis setiap pelanggan
- **Maintenance:** Update model setiap 3 bulan dengan data terbaru

---

## 🛠️ Tools & Teknologi

| Kategori | Tools | Fungsi |
|---|---|---|
| Language | Python 3.x | Bahasa pemrograman utama |
| Data Processing | Pandas, NumPy | Manipulasi & analisis data |
| Visualisasi | Matplotlib, Seaborn | Visualisasi EDA & insights |
| Machine Learning | Scikit-learn | Modeling & evaluasi |
| Model Saving | Pickle | Simpan & load model |
| Environment | Google Colab | Notebook berbasis cloud |

---

## 📁 Struktur Project

```
customer-churn-analysis/
├── notebook/
│   └── Customer_Churn_Analysis.ipynb
├── data/
│   └── E_Commerce_Dataset.xlsx
├── visuals/
│   ├── missing_values.png
│   ├── churn_distribution.png
│   ├── eda_churn_analysis.png
│   ├── model_evaluation.png
│   ├── feature_importance.png
│   └── business_insights.png
├── models/
│   ├── churn_model.pkl
│   └── scaler.pkl
└── README.md
```

---

## 🚀 Cara Menjalankan

```bash
# 1. Clone repository
git clone https://github.com/username/customer-churn-analysis.git
cd customer-churn-analysis

# 2. Install dependencies
pip install pandas numpy matplotlib seaborn scikit-learn openpyxl

# 3. Buka notebook
jupyter notebook notebook/Customer_Churn_Analysis.ipynb
```

### Untuk prediksi pelanggan baru:
```python
import pickle
import pandas as pd

# Load model
with open('models/churn_model.pkl', 'rb') as f:
    model = pickle.load(f)

# Prediksi
prediction = model.predict(new_customer_data)
probability = model.predict_proba(new_customer_data)[:, 1]

print(f"Churn Prediction: {'CHURN' if prediction[0] == 1 else 'TIDAK CHURN'}")
print(f"Churn Probability: {probability[0]:.2%}")
```

---

## 📝 Kesimpulan

Project ini berhasil membangun model prediktif **Customer Churn** yang sangat akurat:

- 🏆 **Random Forest** → Accuracy 98%, ROC-AUC 0.999
- 🎯 Mampu mendeteksi **92% pelanggan churn** sebelum mereka pergi
- 💡 **3 insight utama** yang actionable untuk tim bisnis:
  1. Pelanggan 0–6 bulan adalah segmen paling kritis (churn 25.9%)
  2. Pelanggan yang komplain 3x lebih berisiko churn
  3. Program cashback terbukti efektif untuk retensi

Dengan implementasi rekomendasi bisnis di atas, perusahaan berpotensi **mengurangi churn rate dari 16.8% menjadi di bawah 10%** — berdampak signifikan pada revenue retention.

---
