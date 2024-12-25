
![Ilustrasi Proyek](https://github.com/Wildanamru/Strategi-Optimalisasi-Reservasi-Hotel/blob/main/Visualisasi/Booking%20Now.png)
# 🌟 Strategi Optimalisasi Reservasi Hotel: Analisis Pola Pemesanan dan Faktor Utama Pembatalan 🌟

## 🗂️ Table of Contents
1. [📄 About](#-about)
2. [📦 Package yang diperlukan](#-package-yang-diperlukan)
3. [📊 Sumber Data](#-sumber-data)
4. [🛠️ Proses Pembersihan Data](#-proses-pembersihan-data)
    - [🔍 Identifikasi Nilai NULL](#-identifikasi-nilai-null)
    - [📊 Rekapitulasi Data Sebelum dan Sesudah Pembersihan](#-rekapitulasi-data-sebelum-dan-sesudah-pembersihan)
5. [🔎 EDA (Exploratory Data Analysis)](#-eda-exploratory-data-analysis)
    - [📈 Distribusi Data Pelanggan yang Melakukan Pemesanan Hotel](#distribusi-data-pelanggan-yang-melakukan-pemesanan-hotel)
    - [🌍 Grafik Asal Tamu 10 Teratas](#-grafik-asal-tamu-10-teratas)
    - [👥 Jumlah Tamu Berdasarkan Kategori](#-jumlah-tamu-berdasarkan-kategori)
    - [📉 Pembatalan Berdasarkan Kategori Tamu](#-pembatalan-berdasarkan-kategori-tamu)
    - [🛏️ Jumlah Pelanggan Berdasarkan Tipe Pelanggan](#-jumlah-pelanggan-berdasarkan-tipe-pelanggan)
6. [📊 Analisa Dasar](#-analisa-dasar)
    - [📅 Grafik Jumlah Pemesanan Tiap Bulan](#-grafik-jumlah-pemesanan-tiap-bulan)
    - [🕒 Durasi Rata-rata Pelanggan Menginap](#-durasi-rata-rata-pelanggan-menginap)
    - [🏨 Proporsi Pelanggan Berdasarkan Tipe Hotel](-#proporsi-pelanggan-berdasarkan-tipe-hotel)
7. [📈 Analisis Lanjutan](#-analisis-lanjutan)
    - [✨ Feature Importance](#-feature-importance)
    - [🔗 Analisa Pengaruh Feature deposit_type dan total_of_special_requests terhadap Pembatalan Pemesanan](#-analisa-pengaruh-feature-deposit_type-dan-total_of_special_requests-terhadap-pembatalan-pemesanan)
8. [🎯 Kesimpulan](#-kesimpulan)
9. [📜 Acknowledgment](#-acknowledgment)
10. [✍️ Author](#%EF%B8%8F-author)

---

## 📄 About
Pembatalan pemesanan hotel adalah masalah signifikan yang berdampak pada pendapatan dan efisiensi operasional. Masalah ini memerlukan perhatian serius untuk membantu hotel memahami faktor-faktor utama yang memengaruhi pembatalan dan mengembangkan strategi pencegahan yang efektif.

Penelitian ini menggunakan data pemesanan hotel dari tahun 2015 hingga 2017 dan menggabungkan metodologi Exploratory Data Analysis (EDA) serta Model-Based Feature Selection dengan algoritma Random Forest Classifier. Melalui pendekatan ini, analisis dilakukan untuk menampilkan pola demografis tamu, pola pemesanan, serta mengidentifikasi fitur atau variabel yang paling berpengaruh terhadap pembatalan pemesanan.

💡 Dengan hasil analisis ini, diharapkan dapat memberikan wawasan strategis bagi manajemen hotel terkait penyebab utama pembatalan. Temuan dari penelitian ini memberikan wawasan strategis untuk mengurangi pembatalan, dan menyempurnakan layanan hotel.



## 📦 Package yang diperlukan
Untuk menjalankan analisis ini, pastikan Anda telah menginstal package berikut:

`requests` `pandas` `numpy` `matplotlib` `seaborn` `plotly`

`scikit-learn`

Atau bisa run perintah dibawah ini:
```
bash
  !pip install pandas numpy matplotlib seaborn plotly 
```

---

## 📊 Sumber Data  
Dataset yang digunakan dalam analisis ini diambil dari [ScienceDirect](https://www.sciencedirect.com/science/article/pii/S2352340918315191#f0010) dan mencakup data pemesanan hotel dari tahun 2015 hingga 2017. Dataset ini berisi 32 variabel yang terkait dengan detail pemesanan, termasuk data tamu, karakteristik hotel, dan faktor-faktor yang memengaruhi status reservasi. Dataset "Hotel Bookings" yang sebelumnya digunakan dalam proyek **TidyTuesday** pada 11 Februari 2020, berasal dari penelitian Antonio, Almeida, dan Nunes (2019). Tujuan utama dari dataset ini adalah untuk menganalisis berbagai faktor yang memengaruhi pembatalan pemesanan hotel.  

---

## 🛠️ Proses Pembersihan Data

Dokumen ini menjelaskan proses pembersihan data yang diterapkan pada dataset yang diimpor melalui tautan unduhan dari Dropbox. Dataset tersebut mengandung beberapa nilai **NULL** yang telah diidentifikasi dan ditangani secara sistematis.


### 🔍 Identifikasi Nilai NULL

Pada tahap eksplorasi awal, ditemukan nilai **NULL** pada beberapa variabel berikut:

- **`company`**: 112.593 nilai NULL  
- **`agent`**: 16.340 nilai NULL  
- **`country`**: 488 nilai NULL  
- **`children`**: 4 nilai NULL  

Penanganan nilai **NULL** dilakukan dengan pendekatan yang berbeda sesuai dengan konteks variabel. Untuk variabel `company` dan `agent`, nilai NULL dianggap merepresentasikan pemesanan yang dilakukan secara langsung tanpa keterlibatan perusahaan atau agen eksternal. Oleh karena itu, nilai NULL pada kedua variabel ini diganti dengan kode **1000**, yang berarti "Tanpa Perusahaan" atau "Tanpa Agen". Sementara itu, untuk variabel `country` dan `children`, nilai NULL diputuskan untuk dihapus, karena nilai-nilai tersebut tidak dapat diisi ulang atau dianalisis lebih lanjut secara bermakna.


### 📊 Rekapitulasi Data Sebelum dan Sesudah Pembersihan

Setelah proses pembersihan data, perubahan jumlah nilai NULL dan total data dapat dirangkum sebagai berikut:

| **Variabel**            | **Jumlah Nilai NULL (Sebelum)** | **Jumlah Nilai NULL (Sesudah)** |
|-------------------------|-------------------------------|----------------------------------|
| `children`              | 4                            | 0                                |
| `country`               | 488                          | 0                                |
| `company`               | 112.593                      | 0                                |
| `agent`                 | 16.340                       | 0                                |
| **Total Data Keseluruhan** | **119.390**                 | **118.898**                      |


Penggantian nilai NULL pada variabel `agent` dan `company` memberikan wawasan penting bahwa mayoritas pemesanan dilakukan langsung tanpa keterlibatan agen atau perusahaan, yang tercermin dari tingginya proporsi nilai **1000** setelah pembersihan. Sementara itu, penghapusan nilai NULL pada `country` dan `children` tidak memengaruhi kualitas data secara keseluruhan, karena jumlahnya kurang dari 1% dari total dataset. Setelah proses pembersihan, jumlah data yang dapat dianalisis berkurang dari **119.390** menjadi **118.898** baris, memastikan dataset lebih bersih dan siap untuk analisis lebih lanjut dengan hasil yang lebih akurat.

---



## 🔎 EDA (Exploratory Data Analysis)

Langkah awal dalam analisis ini adalah melakukan eksplorasi data (EDA) untuk memahami karakteristik dasar dataset. Proses ini meliputi analisis distribusi data, eksplorasi pola-pola awal seperti kategori pengunjung, tipe customer, durasi rata rata pelanggan menginap, proporsi tamu. Visualisasi data seperti histogram, diagram batang, digunakan untuk mendukung analisis ini.

### 📈 Distribusi Data Pelanggan yang Melakukan Pemesanan Hotel 
|Status Pemesanan               | Jumlah                                   |
|-------------------------------|------------------------------------------|
| `Not Cancelation (0)`         | 74.745                                   |  
| `Cancelation (1)`             | 44.153                                   |  

Tabel di atas menunjukkan distribusi status pembatalan pemesanan hotel dari tahun 2015 hingga 2017. Dari tabel ini, terlihat bahwa jumlah pemesanan yang tidak dibatalkan (kategori 0) jauh lebih tinggi dibandingkan dengan pemesanan yang dibatalkan (kategori 1). Secara keseluruhan, terdapat lebih dari 70.000 pemesanan yang berhasil terlaksana, sementara pembatalan hanya terjadi pada sekitar 40.000 pemesanan. Perbedaan ini menunjukkan bahwa meskipun pembatalan menjadi masalah signifikan, sebagian besar tamu tetap melanjutkan reservasi mereka, memberikan peluang untuk lebih memahami pola dan faktor yang memengaruhi pembatalan tersebut.grafik bisa dilihat pada code

### 🌍 Grafik Asal Tamu 10 Teratas

![top 10](https://github.com/BAGUSW6/analisisbigdata/blob/main/visualisasi/newplot%20(12).png)

### 👥 Jumlah Tamu Berdasarkan Kategori

| Kategori | Jumlah Tamu |
|----------|-------------|
| Adults   | 136,965     |
| Children | 7,680       |
| Babies   | 776         |

Antara tahun 2015 hingga 2017, mayoritas tamu berasal dari Portugal (PRT) dengan lebih dari 20.000 kunjungan tanpa pembatalan, diikuti oleh Inggris (GBR) dan Prancis (FRA). Selain itu, mayoritas tamu secara keseluruhan berasal dari kategori dewasa (adults) dengan jumlah 136,965, sementara kategori anak-anak (children) dan bayi (babies) memiliki kontribusi yang jauh lebih kecil. Data ini mencerminkan bahwa perjalanan wisata didominasi oleh orang dewasa, dengan Portugal sebagai negara asal tamu terbesar, kemungkinan karena faktor geografis, budaya, dan aksesibilitas.

---

### 📉 Pembatalan Berdasarkan Kategori Tamu

![kategori tamu](https://github.com/BAGUSW6/analisisbigdata/blob/main/visualisasi/newplot%20(14).png)

Terlihat bahwa kategori tamu Personal memiliki jumlah pemesanan yang jauh lebih tinggi dibandingkan Company, namun juga lebih banyak mengalami pembatalan. Hal ini menunjukkan bahwa tamu personal lebih mendominasi pasar, mungkin karena mereka lebih fleksibel dalam membuat keputusan perjalanan, sementara tamu dari Company cenderung memiliki rencana yang lebih terstruktur dan jarang membatalkan pemesanan.

### 🛏️ Jumlah Pelanggan Berdasarkan Tipe Pelanggan 

| Tipe Pelanggan  |Jumlah Pelanggan |
|-----------------|-----------------|
| Transient       | 52,714          |
| Transient-Party | 18,705          |
| Contract        | 2,814           |
| Group           | 512             |


Tamu dari kategori Personal dominan pada tipe pelanggan Transient dan Transient-Party, mencerminkan pemesanan fleksibel oleh individu atau kelompok kecil. Sebaliknya, tamu Company lebih sering terkait dengan tipe pelanggan Contract, karena sifat pemesanan yang terencana. Tipe Group, meski paling sedikit, mencakup tamu Personal dan Company, namun lebih terorganisir dan spesifik. Pola ini menunjukkan hubungan erat antara tujuan perjalanan dan preferensi pemesanan.



## 📊 Analisa Dasar


### 📅 Grafik jumlah pemesanan tiap bulan

![jumlah pesanan tiap bulan](https://github.com/BAGUSW6/analisisbigdata/blob/main/visualisasi/newplot%20(16).png)

Visualisasi ini menunjukkan jumlah pemesanan per bulan untuk pemesanan yang tidak dibatalkan. Puncak pemesanan terjadi pada bulan Agustus, dengan jumlah lebih dari 8.000, menjadikannya bulan tersibuk. Bulan-bulan lain seperti Juni, Juli, dan September juga menunjukkan jumlah pemesanan yang tinggi, mengindikasikan musim liburan musim panas sebagai periode favorit pelanggan. Sebaliknya, bulan November dan Desember memiliki jumlah pemesanan paling rendah, mencerminkan periode yang mungkin kurang diminati untuk perjalanan. Pola ini menunjukkan bahwa tren pemesanan sangat dipengaruhi oleh musim dan preferensi waktu liburan.

### 🕒 Durasi rata-rata Pelanggan Menginap

![rata-rata Pelanggan Menginap](https://github.com/BAGUSW6/analisisbigdata/blob/main/visualisasi/newplot%20(18).png)

Visualisasi ini menunjukkan rata-rata durasi menginap (dalam malam) berdasarkan tipe pelanggan dan jenis hotel untuk pemesanan yang tidak dibatalkan. Pelanggan Contract memiliki rata-rata durasi menginap tertinggi, terutama di Resort Hotel dengan rata-rata sekitar 10 malam, diikuti oleh City Hotel dengan durasi lebih pendek. Pelanggan Group dan Transient memiliki rata-rata durasi yang lebih rendah, dengan sebagian besar waktu dihabiskan di Resort Hotel dibandingkan City Hotel. Pelanggan Transient-Party memiliki durasi menginap paling singkat di kedua jenis hotel. Data ini mencerminkan bahwa pelanggan tipe Contract cenderung memesan untuk jangka waktu lebih lama, kemungkinan untuk keperluan kerja atau acara tertentu, sementara pelanggan tipe lainnya cenderung memesan untuk perjalanan yang lebih singkat, terutama di City Hotel.


### 🏨 Proporsi Pelanggan berdasarkan tipe Hotel

![Proporsi Pelanggan berdasarkan tipe Hotel](https://github.com/BAGUSW6/analisisbigdata/blob/main/visualisasi/newplot%20(19).png)

Visualisasi ini mengungkap pola pembatalan reservasi pada dua tipe hotel, yaitu **City Hotel** dan **Resort Hotel**, dengan kategori status reservasi **Not Canceled** dan **Canceled**. Pada City Hotel, jumlah pembatalan cukup tinggi meskipun reservasi yang tidak dibatalkan tetap mendominasi, yang dapat mengindikasikan tantangan dalam mempertahankan komitmen pelanggan. Sebaliknya, Resort Hotel menunjukkan tingkat pembatalan yang lebih rendah secara absolut, meskipun reservasi yang tidak dibatalkan juga lebih tinggi. Temuan ini memberikan indikasi bahwa City Hotel mungkin memerlukan strategi khusus untuk mengurangi pembatalan, seperti peningkatan pengalaman pelanggan atau pengelolaan ekspektasi, sementara Resort Hotel tampak lebih efektif dalam mempertahankan reservasi.


## 📈 Analisis Lanjutan

### ✨ Feature Importance

Untuk mendukung analisis ini, berikut disajikan tabel dan visualisasi *feature importance* yang menunjukkan kontribusi masing-masing fitur terhadap model prediksi. Tabel memberikan rincian numerik tentang tingkat pengaruh setiap fitur, sementara grafik batang memvisualisasikan peringkat fitur untuk memudahkan interpretasi. 

### Tabel Feature Importance

| Rank | Feature                       | Importance |
|------|-------------------------------|------------|
| 1    | ADR (Average Daily Rate)      | 29.5%      |
| 2    | Lead Time                     | 28.9%      |
| 3    | Deposit Type (Non Refund)     | 14.5%      |
| 4    | Total Special Requests        | 6.2%       |
| 5    | Previous Cancellations        | 5.1%       |

### Visualisasi Feature Importance

![Feature Importance](https://github.com/BAGUSW6/analisisbigdata/blob/main/visualisasi/ppp.png)


Analisis menggunakan Random Forest Classifier berhasil mengidentifikasi faktor-faktor utama yang memengaruhi pembatalan reservasi hotel, dengan akurasi model mencapai 83%. Hasilnya menunjukkan bahwa ADR (Average Daily Rate), lead_time, dan deposit_type (Non Refund) merupakan fitur yang paling berpengaruh, diikuti oleh jumlah permintaan khusus dan pembatalan sebelumnya. Visualisasi feature importance menunjukkan bahwa fokus pada fleksibilitas harga, insentif untuk deposit, dan pengelolaan ekspektasi pelanggan dapat menjadi strategi efektif untuk mengurangi pembatalan. Temuan ini memberikan dasar yang kuat untuk pengambilan keputusan berbasis data dalam meningkatkan kinerja bisnis hotel.

### 🔗Analisa pengaruh Feature deposit_type dan total_of_special_requests terhadap Pembatalan Pemesanan

Analisis lanjutan difokuskan pada deposit_type dan total_of_special_requests karena keduanya memiliki relevansi strategis yang kuat dalam mengurangi risiko pembatalan. Deposit_type (Non Refund) menunjukkan pengaruh signifikan, di mana kebijakan deposit tanpa pengembalian berhubungan erat dengan pembatalan, kemungkinan akibat kurangnya fleksibilitas yang dirasakan pelanggan. Sementara itu, total_of_special_requests mengindikasikan bahwa semakin banyak permintaan khusus yang diajukan, semakin kecil kemungkinan pembatalan, karena pelanggan yang terlibat lebih cenderung melanjutkan reservasi. Dibandingkan dengan ADR dan lead_time, yang bersifat lebih prediktif, kedua fitur ini memberikan peluang lebih besar untuk diintervensi secara operasional, seperti melalui fleksibilitas kebijakan deposit dan pengelolaan permintaan khusus, guna meningkatkan pengalaman pelanggan dan mengurangi tingkat pembatalan.

![distribusi deposito](https://github.com/BAGUSW6/analisisbigdata/blob/main/visualisasi/newplot%20(20).png)

![pembatalan berdasarkan deposito](https://github.com/BAGUSW6/analisisbigdata/blob/main/visualisasi/newplot%20(21).png)

Visualisasi pertama menunjukkan bahwa mayoritas pelanggan memilih pemesanan tanpa memberikan deposit (**No Deposit**), sementara visualisasi kedua mengungkapkan bahwa tipe ini memiliki tingkat pembatalan yang signifikan meskipun sebagian besar reservasi tetap dilanjutkan. Sebaliknya, pada tipe **Non Refund**, pembatalan jauh lebih rendah, yang mencerminkan pengaruh kebijakan deposit terhadap komitmen pelanggan. Untuk mengatasi tingginya tingkat pembatalan pada **No Deposit**, hotel dapat menawarkan insentif pada opsi **Non Refund**, seperti diskon harga atau layanan tambahan, guna meningkatkan daya tariknya. Selain itu, pengenalan kebijakan hybrid, seperti deposit sebagian dengan pengembalian sebagian, dapat menyeimbangkan kebutuhan fleksibilitas pelanggan dengan pengurangan pembatalan. Langkah-langkah ini, jika dipadukan dengan segmentasi pelanggan dan evaluasi berkala, dapat membantu hotel meningkatkan komitmen pelanggan dan menurunkan tingkat pembatalan secara signifikan.

![distribusi special request](https://github.com/BAGUSW6/analisisbigdata/blob/main/visualisasi/newplot%20(22).png)

![pembatalan berdasarkan request](https://github.com/BAGUSW6/analisisbigdata/blob/main/visualisasi/newplot%20(23).png)

Visualisasi pertama menunjukkan bahwa pelanggan dengan **0 permintaan khusus** memiliki tingkat pembatalan tertinggi, sementara semakin banyak permintaan khusus yang diajukan, tingkat pembatalan cenderung menurun, mencerminkan keterlibatan pelanggan yang lebih tinggi. Visualisasi kedua mengungkapkan bahwa mayoritas pelanggan tidak mengajukan permintaan khusus, sedangkan sebagian kecil mengajukan 1 hingga 2 permintaan. Untuk mengurangi pembatalan, hotel dapat mendorong keterlibatan pelanggan dengan memfasilitasi permintaan khusus melalui komunikasi proaktif selama pemesanan, meningkatkan personalisasi layanan, dan memastikan sistem hotel mampu mencatat serta memenuhi permintaan ini secara efisien. Selain itu, hotel dapat mengevaluasi pola pembatalan dari pelanggan yang tidak mengajukan permintaan khusus untuk mengembangkan strategi mitigasi yang lebih efektif.


## 🎯 Kesimpulan

Pembatalan reservasi hotel merupakan masalah signifikan yang berdampak pada pendapatan dan efisiensi operasional, terutama pada kategori pemesanan tertentu. Penelitian ini menggunakan dataset pemesanan hotel tahun 2015-2017 dengan 32 variabel, memanfaatkan metodologi Exploratory Data Analysis (EDA) dan Random Forest Classifier untuk memahami pola data dan mengidentifikasi faktor-faktor utama yang memengaruhi pembatalan, seperti deposit_type, total_of_special_requests, ADR, dan lead_time. Analisis menemukan bahwa mayoritas pembatalan terjadi pada pemesanan tanpa deposit (No Deposit), sementara deposit_type Non Refund memiliki tingkat pembatalan jauh lebih rendah. Selain itu, pelanggan dengan 0 permintaan khusus memiliki tingkat pembatalan tertinggi, sedangkan semakin banyak permintaan khusus diajukan, pembatalan cenderung menurun. Puncak pemesanan terjadi pada bulan liburan seperti Agustus, dengan tingkat pembatalan yang lebih tinggi di City Hotel dibandingkan Resort Hotel. Implikasi analisis ini mendorong hotel untuk mengadopsi kebijakan Non Refund dengan insentif, meningkatkan keterlibatan pelanggan melalui permintaan khusus, dan mengoptimalkan pengalaman di City Hotel untuk menurunkan pembatalan. Namun, analisis ini terbatas pada data historis 2015-2017 dan tidak mencakup faktor eksternal seperti kondisi ekonomi atau persaingan industri. Untuk pengembangan lebih lanjut, analisis dapat mencakup data real-time, ulasan pelanggan, atau faktor eksternal guna memberikan wawasan yang lebih relevan dan strategis.

## 📜 Acknowledgment
Visualisasi dan analisis ini dibuat berdasarkan data dari

[![ScienceDirect](https://img.shields.io/badge/Dataset-ScienceDirect-blue)](https://www.sciencedirect.com/science/article/pii/S2352340918315191#f0010)

Semua kode tersedia di 

[![Open Colab](https://img.shields.io/badge/Notebook-Colab-green)](https://colab.research.google.com/drive/13tV-R2nSngDVyNmIW7pcxmyaxqE6a35J?usp=sharing)


## ✍️ Author  
Dokumen ini dibuat oleh tim yang berdedikasi tinggi dengan semangat kerja sama untuk menyelesaikan analisis ini:

| **Nama**                   | **Nomor Absen** | 
|----------------------------|-----------------|
|  **Naufal Angling D**    |202110370311066  | 
|  **Bagus Wicaksono**     |202110370311220  |
|  **Wildan Amru Hidayat** |202110370311280  | 

 _Tim ini berkomitmen untuk menghadirkan analisis data yang bermanfaat dan relevan. Setiap anggota memiliki kontribusi unik untuk menciptakan hasil terbaik._
