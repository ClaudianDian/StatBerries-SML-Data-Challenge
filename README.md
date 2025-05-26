
<p align="center">
  <img width="1000" height="250" src="Image/logo-ipb.png">
</p>

<div align="center">

# 🍓 DATA SCIENCE CHALLENGE - STATBERRIES 🍓
---
# PREDIKSI RISIKO RENDAHNYA KONVERGENSI IBU ANAK UNTUK PENANGGULANGAN STUNTING
---

[Tentang](#clipboard-Tentang) - [Tujuan dan Fokus](#dart-Tujuan-danFokus) - [Data](#books-Data) - [Diagram Alir](#jigsaw-Diagram-Alir) -[Modeling](#computer-Modeling) - [Evaluasi](#bar_chart-Evaluasi) - [Team](#busts_in_silhouette-Team)
</div>

## :clipboard: Tentang
### **Deskripsi Singkat**
Proyek ini bertujuan untuk memprediksi risiko rendahnya konvergensi layanan dasar yang diterima oleh ibu hamil, bayi, dan balita dalam upaya penanggulangan stunting di Indonesia. Konvergensi layanan mencakup intervensi kesehatan, gizi, sanitasi, pendidikan, dan perlindungan sosial yang terintegrasi di tingkat desa. Dengan menggunakan data tingkat desa tahun 2022, proyek ini memodelkan potensi kegagalan konvergensi melalui pendekatan analitik dan visualisasi interaktif. Sistem ini dirancang untuk mendukung pengambilan kebijakan berbasis data, sehingga intervensi dapat diarahkan secara lebih tepat sasaran pada wilayah dan kelompok masyarakat yang paling membutuhkan.

## :dart: Tujuan dan Fokus
### **Tujuan**
Proyek ini bertujuan untuk mengembangkan sistem prediksi risiko rendahnya tingkat konvergensi layanan ibu dan anak di wilayah desa, sebagai bagian dari upaya mendukung kebijakan percepatan penurunan stunting di Indonesia. Sistem ini dirancang agar dapat memberikan gambaran visual dan analisis risiko berbasis data, sehingga mempermudah pemangku kebijakan dalam mengidentifikasi wilayah atau kelompok sasaran yang membutuhkan intervensi prioritas.
### **Fokus**
1. Analisis Data Konvergensi: Mengolah data indikator layanan dasar yang diterima oleh ibu hamil, bayi, dan balita pada tingkat desa.
2. Pemodelan Prediktif: Menggunakan pendekatan machine learning untuk memprediksi risiko rendahnya konvergensi layanan.
3. Visualisasi Interaktif: Menyajikan hasil analisis dalam bentuk visualisasi dashboard HTML yang mudah dipahami.
4. Pendukung Kebijakan: Memberikan output yang aplikatif sebagai bahan pertimbangan dalam perencanaan dan evaluasi program intervensi stunting oleh pemerintah daerah atau pusat.

## :books: Data
### **Sumber Data**
Data yang digunakan dalam proyek ini diperoleh dari portal resmi pemerintah Indonesia, yaitu data.go.id, melalui dataset berjudul **Data Stunting Tahun 2022**. Dataset ini disusun dan dipublikasikan oleh Kementerian Desa, Pembangunan Daerah Tertinggal, dan Transmigrasi Republik Indonesia, sejalan dengan amanat Peraturan Presiden Republik Indonesia Nomor 72 Tahun 2021 tentang Percepatan Penurunan Stunting.  
Sumber data : https://data.go.id/dataset/dataset/data-stunting-2022
### Tahun dan Cakupan
Tahun data : 2022  
Cakupan geografis : Provinsi di Pulau Jawa (DKI Jakarta, Banten, Jawa Barat, Jawa Tengah, DI Yogyakarta & Jawa Timur)  
Unit observasi : Desa/Kelurahan  
Jumlah observasi : 22475  
Jumlah variabel : 44  

Data ini memuat informasi tahun 2022 pada tingkat desa/kelurahan, yang mencakup:
1. Status penerimaan layanan dasar oleh ibu hamil, bayi, dan balita
2. Indikator akses terhadap fasilitas kesehatan, gizi, dan lingkungan
3. Identifikasi risiko rendahnya konvergensi
Dataset ini menjadi dasar dalam membangun sistem prediktif untuk mengidentifikasi desa-desa dengan risiko konvergensi rendah, guna mendukung target nasional penurunan stunting hingga 14% pada tahun 2024.
### Exploratory Data Analysis (EDA)
Tahapan EDA dilakuka untuk memahami pola distribusi, hubungan antar variabel, serta karakteristik data berdasarkan risiko stunting.  
#### Distribusi Kelas Target stunting_risk
78,87% desa berada dalam kategori risiko **rendah** dan 21,13% desa berada dalam kategori risiko **tinggi**.  
Ketidakseimbangan kelas ini perlu dipertimbangkan dalam pemodelan karena dapat memengaruhi performa model klasifikasi.
#### Boxplot Berdasarkan Risiko
Boxplot per kategori stunting_risk memperlihatkan perbedaan distribusi yang signifikan untuk sejumlah variabel :  
1. Desa risiko **rendah** cenderung memiliki nilai lebih tinggi pada variabel layanan, seperti Anak_Timbang_Rutin, Jlh_Anak_JamKes, dan Anak_Imunisasi
2. Desa risiko **tinggi** menunjukkan lebih banyak nilai rendah atau nol, menunjukkan **kesenjangan layanan**
#### Korelasi Antar Variabel
Heatmap korelasi mengindikasikan adanya korelasi sedang hingga kuat antar indikator layanan dasar yang memiliki jenis layanan serupa, misalnya korelasi positif antara Bumil_cek_4kali dan Bumil_Konseling_Gizi_4kali.  
<p align="center">
  <img width="700" height="500" src="EDA/Korelasi.png">
</p>
Grafik EDA dapat ditemukan pada folder EDA di repository ini.

## :jigsaw: Diagram Alir
<p align="center">
  <img width="900" height="500" src="Image/Blank diagram.png">
</p>

## :computer: Modeling
### Pembagian Data
Dalam proses pelatihan dan pengujian model, digunakan dua skema pembagian data untuk mengevaluasi stabilitas dan keandalan performa model klasifikasi :  
**1. Skema 80:20**
 - 80% data latih digunakan untuk membangun model
 - 20% data uji digunakan untuk mengevaluasi performa generalisasi model

**2. Skema 70:30**
 - 70% data latih digunakan untuk membangun model
 - 30% data uji digunakan untuk mengevaluasi performa generalisasi model
### Skenario Pengaturan Fitur
Kemudian setiap skema pembagian data diuji dalam dua skenario pengaturan fitur, yaitu:
1. **Skenario Full Fitur**, menggunakan seluruh variabel yang ada dengan mengecualikan variabel yang mengandung informasi target secara eksplisit (untuk menghindari *data leakage*).
2. **Skenario Top 14 Fitur**, menggunakan 14 fitur paling relevan berdasarkan korelasi dan interpretasi model setelah dilakukan pemodelan pada skenaro full fitur.

### Perbandingan Imbalanced & Balanced Data
Distribusi kelas stunting risk pada dataset tergolong tidak seimbang. Oleh karena itu dilakukan eksperimen dengan mengggunakan metode **SMOTE (Synthetic Minority Over-sampling Technique)** yang bertujuan untuk meningkatkan sensitivitas model terhadap kelas minoritas tanpa menurunkan performa secara keseluruhan.

### Model yang Digunakan
**1. K-Nearest Neighbour (KNN)**
- Metode instance-based yang mengklasifikasikan data berdasarkan tetangga terdekatnya.
- Hyperparameter tuning dilakukan terhadap nilai k menggunakan cross-validation.
  
**2. Regresi Logistik**
- Model probabilistik yang mengasumsikan hubungan log-linear antara fitur dan log odds dari kelas target.
- Dapat digunakan untuk interpretasi pengaruh fitur melalui koefisien.
  
**3. C5.0 Desicion Tree**
- Pohon keputusan yang menghasilkan model interpretable dan mendukung feature importance scoring.
- Digunakan juga dengan SMOTE untuk melihat pengaruh balancing terhadap performa.

### Preprocessing Data
- Winsorizing diterapkan untuk membatasi pengaruh outlier ekstrim. Nilai-nilai ekstrim dari setiap variabel numerik dipotong pada persentil bawah dan atas.
- Data bersifat imbalanced sehingga digunakan metode SMOTE (Synthetic Minority Over-sampling Technique) pada data latih.

## :bar_chart: Evaluasi
Setiap model dievaluasi menggunakan empat metrik utama:
- **Accuracy**
- **F1-Score**
- **Kappa Statistic**
- **Balanced Accuracy**
  
### 📊 Skema 70:30
#### 1. Full Fitur
| Model            | Accuracy | F1 Score | Kappa | Balanced Accuracy |
|------------------|----------|----------|--------|--------------------|
| **C5.0 (Full)**  | 97.42%   | 0.984    | 0.923  | 96.28%             |
| Logistic (Full)  | 90.48%   | 0.942    | 0.687  | 81.31%             |
| KNN (Full)       | 84.02%   | 0.900    | 0.504  | 74.40%             |

#### 2. Top 14 Fitur
| Model                | Accuracy | F1 Score | Kappa | Balanced Accuracy |
|----------------------|----------|----------|--------|--------------------|
| **C5.0 (14 Fitur)**  | 93.19%   | 0.957    | 0.793  | 89.09%             |
| Logistic (14 Fitur)  | 85.91%   | 0.915    | 0.503  | 71.39%             |
| KNN (14 Fitur)       | 86.98%   | 0.915    | 0.633  | 83.72%             |

Dari hasil perbandingan performa model dengan menggunakan skenario full fitur dan top 14 fitur diperoleh model terbaik adalah model C5.0 Full fitur dengan akurasi tertinggi yaitu sebesar 97.42%. Kemudian dilakukan analisis feature importance untuk mengidentifikasi variabel mana yang memberikan kontribusi terbesar dalam klasifikasi tingkat risiko stunting.
<p align="center">
  <img width="700" height="500" src="Image/Feature Importance 70-30.jpg">

  
#### 3. Full Fitur with SMOTE
| Model                  | Accuracy | F1 Score | Kappa | Balanced Accuracy |
|------------------------|----------|----------|--------|--------------------|
| **C5.0 (SMOTE Full)**  | 97.40%   | 0.9834   | 0.9226 | 96.57%             |
| Logistic (SMOTE Full)  | 96.36%   | 0.9314   | 0.7205 | 90.10%             |
| KNN (SMOTE Full)       | 72.34%   | 0.7991   | 0.3843 | 75.09%             |

#### 4. Top 14 Fitur with SMOTE
| Model                   | Accuracy | F1 Score | Kappa | Balanced Accuracy |
|-------------------------|----------|----------|--------|--------------------|
| **C5.0 (SMOTE 14 Fitur)** | 92.22%   | 0.9498   | 0.7784 | 90.99%             |
| Logistic (SMOTE 14)     | 84.36%   | 0.8949   | 0.5939 | 84.30%             |
| KNN (SMOTE 14)          | 81.49%   | 0.8708   | 0.5557 | 84.74%             |

Tabel di atas menunjukkan bahwa model C5.0 consistently memberikan performa terbaik dalam skenario SMOTE, baik dengan full fitur maupun top 14 fitur, dengan akurasi dan F1 Score tertinggi. Sementara itu, model KNN menunjukkan performa terendah, terutama pada skenario full fitur, yang mengindikasikan sensitivitas model ini terhadap distribusi data dan fitur yang digunakan.

<p align="center">
  <img width="700" height="500" src="Image/Feature Importance 70-30 + SMOTE.jpg">
  
### 📊 Skema 80:20
#### 1. Full Fitur
| Model            | Accuracy | F1 Score | Kappa | Balanced Accuracy |
|------------------|----------|----------|--------|--------------------|
| **C5.0 (Full)**  | 97.05%   | 0.981    | 0.912  | 95.80%             |
| Logistic (Full)  | 91.48%   | 0.947    | 0.727  | 84.00%             |
| KNN (Full)       | 84.20%   | 0.901    | 0.515  | 75.20%             |

#### 2. Top 14 Fitur
| Model                | Accuracy | F1 Score | Kappa | Balanced Accuracy |
|----------------------|----------|----------|--------|--------------------|
| **C5.0 (14 Fitur)**  | 93.03%   | 0.956    | 0.790  | 89.50%             |
| Logistic (14 Fitur)  | 87.15%   | 0.922    | 0.556  | 74.10%             |
| KNN (14 Fitur)       | 86.44%   | 0.911    | 0.627  | 84.20%             |

Model C5.0 dengan skenario full fitur menunjukkan performa terbaik dengan akurasi 97.05% dan F1 Score 0.981, mengungguli model lainnya. Hal ini menandakan bahwa penggunaan seluruh fitur memberikan kontribusi signifikan terhadap kemampuan model dalam mengklasifikasikan risiko stunting secara akurat.

<p align="center">
  <img width="700" height="500" src="Image/Feature Importance 80-20.jpg">
  
#### 3. Full Fitur with SMOTE
| Model                  | Accuracy | F1 Score | Kappa | Balanced Accuracy |
|------------------------|----------|----------|--------|--------------------|
| **C5.0 (SMOTE Full)**  | 97.23%   | 0.9823   | 0.9171 | 96.42%             |
| Logistic (SMOTE Full)  | 90.34%   | 0.9357   | 0.7438 | 91.98%             |
| KNN (SMOTE Full)       | 70.82%   | 0.7855   | 0.3639 | 75.05%             |

#### 4. Top 14 Fitur with SMOTE
| Model                   | Accuracy | F1 Score | Kappa | Balanced Accuracy |
|-------------------------|----------|----------|--------|--------------------|
| **C5.0 (SMOTE 14 Fitur)** | 92.81%   | 0.9537   | 0.7928 | 91.92%             |
| Logistic (SMOTE 14)     | 84.85%   | 0.8992   | 0.5975 | 83.76%             |
| KNN (SMOTE 14)          | 82.27%   | 0.8773   | 0.5668 | 84.82%             |

Model C5.0 dengan SMOTE dan full fitur kembali menjadi yang terbaik dengan akurasi 97.23% dan F1 Score 0.9823, menunjukkan kinerja sangat unggul meski data seimbang. Sementara itu, performa KNN masih tertinggal signifikan di kedua skenario, terutama dalam akurasi dan kappa.

<p align="center">
  <img width="700" height="500" src="Image/Feature Importance 80-20 +SMOTE.jpg">


### 📊 Perbandingan Performa Model Berdasarkan Skema Split Data

| Model                     | Split 70:30                     | Split 80:20                     |
|                           |---------------------------------|---------------------------------|
|                           | 70:30 Accuracy | 70:30 F1 Score | 80:20 Accuracy | 80:20 F1 Score |
|---------------------------|----------------|----------------|----------------|----------------|
| **C5.0 (Full)**           | **97.42%**     | **0.984**      | **97.05%**     | **0.981**      |
| Logistic (Full)           | 90.48%         | 0.942          | 91.48%         | 0.947          |
| KNN (Full)                | 84.02%         | 0.900          | 84.20%         | 0.901          |
| **C5.0 (Top 14 Fitur)**   | 93.19%         | 0.957          | 93.03%         | 0.956          |
| Logistic (Top 14)         | 85.91%         | 0.915          | 87.15%         | 0.922          |
| KNN (Top 14)              | 86.98%         | 0.915          | 86.44%         | 0.911          |
| **C5.0 (SMOTE Full)**     | 97.40%         | 0.9834         | 97.23%         | 0.9823         |
| Logistic (SMOTE Full)     | 96.36%         | 0.9314         | 90.34%         | 0.9357         |
| KNN (SMOTE Full)          | 72.34%         | 0.7991         | 70.82%         | 0.7855         |
| **C5.0 (SMOTE 14 Fitur)** | 92.22%         | 0.9498         | 92.81%         | 0.9537         |
| Logistic (SMOTE 14)       | 84.36%         | 0.8949         | 84.85%         | 0.8992         |
| KNN (SMOTE 14)            | 81.49%         | 0.8708         | 82.27%         | 0.8773         |

Berdasarkan hasil pemodelan dengan total 24 skenario model, diperoleh model terbaik yaitu C5.0 dengan menggunakan full fitur dan SMOTE. Model ini mencatat akurasi tertinggi sebesar 97.23%, F1 Score 0.9823, Kappa 0.9171, dan balanced accuracy 96.42%, menjadikannya paling andal dalam membedakan kategori risiko stunting secara konsisten dan seimbang. <br>
Dari grafik feature importance model C5.0 (SMOTE Full), dapat disimpulkan bahwa beberapa variabel memiliki kontribusi dominan dalam klasifikasi risiko stunting yaitu Usia Anak 0-23 Bulan yang menjadi fitur paling penting (skor = 100). Hal ini menunjukkan bahwa usia sangat menentukan status pertumbuhan anak dan pengaruhnya terhadap risiko stunting. Kemudian Anak_Timbang_Rutin (95.3) menandakan bahwa kegiatan pemantauan tumbuh kembang anak melalui penimbangan rutin sangat krusial dalam mendeteksi risiko. Akses terhadap Air Minum Aman (82.41) dan Jlh_Anak_Punya_Akta_Lahir (78.17) serta Anak_Ukur_Panjang (76.68) dan Jlh_Anak_JamKes (75.65) memperkuat bahwa aspek pengukuran fisik serta jaminan kesehatan sangat mempengaruhi klasifikasi.<br>
Hal ini menunjukkan bahwa Intervensi kebijakan sebaiknya difokuskan pada aspek gizi anak usia dini, akses lingkungan sehat, dan cakupan layanan dasar seperti pemantauan tumbuh kembang dan jaminan kesehatan. Model machine learning seperti C5.0 dapat menjadi alat bantu strategis untuk pemetaan wilayah prioritas dan alokasi program pencegahan stunting berbasis data.<br>

## 📄 Kesimpulan
1. Model C5.0 konsisten unggul dalam seluruh skenario, dengan performa akurasi dan F1 Score tertinggi. Model ini menunjukkan keunggulan baik dalam hal generalisasi maupun kestabilan prediksi.
2. Penerapan SMOTE berhasil meningkatkan performa klasifikasi, terutama untuk model yang sensitif terhadap imbalance seperti KNN dan Regresi Logistik.
3. Seleksi fitur efektif mempertahankan performa. Dengan hanya 14 fitur utama, model tetap mampu mencapai akurasi lebih dari 90%, menunjukkan bahwa sebagian besar informasi penting terkandung pada subset fitur tersebut.
4. Skema split 80:20 sedikit lebih stabil dibanding 70:30 dalam menghasilkan performa yang optimal pada data uji, terutama saat digunakan bersamaan dengan balancing dan fitur lengkap.
   
## 💡 Insight
Berdasarkan analisis feature importance dan performa model klasifikasi, berikut rekomendasi strategis untuk pembangunan dan intervensi pengentasan stunting:
1. Program konvergensi stunting perlu difokuskan pada desa-desa yang menunjukkan nilai rendah dalam indikator utama seperti penimbangan rutin anak, akses air minum dan sanitasi layak, konseling gizi bagi ibu hamil, partisipasi pengasuh dalam parenting dan Cakupan Rumah Tangga 1.000 HPK.
2. Model klasifikasi berbasis machine learning terbukti efektif untuk mengidentifikasi wilayah dengan risiko tinggi secara lebih presisi. Hal ini mendukung pengambilan kebijakan yang tepat sasaran, efisien dalam alokasi anggaran dan sumber daya dan responsif terhadap data lapangan
3. Pemerintah daerah & Dinas Kesehatan dapat menggunakan model ini sebagai sistem pendukung keputusan untuk perencanaan program gizi dan sanitasi berbasis desa.
4. Tim Program Nasional Pencegahan Stunting dapat memprioritaskan intervensi berbasis indikator yang paling memengaruhi risiko.
5. Akademisi dan Peneliti dapat mengembangkan metode lanjutan yang lebih adaptif, integratif, dan berbasis data longitudinal serta spasial.
   
## :busts_in_silhouette: Team

| Nama Lengkap               | NIM           |
|----------------------------|---------------|
| Fani Fahira                | M0501241052   |
| Claudian T. Tangdilomban  | M0501241048   |
| Sabrina Adnin Kamila      | M0501241042   |
| Baiq Nina Febrina         | M0501241063   |
