# **Strategi Optimalisasi Reservasi Hotel: Analisis Pola Pemesanan dan Faktor Utama Pembatalan**  
*(“Meningkatkan Keberhasilan Reservasi dengan Pendekatan Data dan Solusi Berbasis Wawasan”)*  

---

## **Bab 1: About**  
### 💼 **Pendahuluan**  
Pembatalan pemesanan hotel adalah salah satu tantangan utama dalam industri perhotelan. Dampaknya tidak hanya mengurangi pendapatan, tetapi juga memengaruhi efisiensi operasional hotel. Untuk itu, diperlukan pendekatan berbasis data guna memahami akar masalah pembatalan dan merumuskan strategi pencegahan yang efektif.

### 🌐 **Highlight Penelitian**  
Penelitian ini menggunakan data dari tahun 2015-2017 dengan kombinasi **Exploratory Data Analysis (EDA)** dan **Model-Based Feature Selection** menggunakan algoritma **Random Forest Classifier**. Dengan pendekatan ini, pola demografis, pola pemesanan, serta variabel penting yang memengaruhi pembatalan berhasil diidentifikasi.

### 🎯 **Tujuan**  
Hasil analisis diharapkan memberikan wawasan strategis bagi hotel untuk:  
- Mengurangi tingkat pembatalan  
- Meningkatkan efisiensi operasional  
- Meningkatkan kualitas pengalaman pelanggan  

---

## **Bab 2: Package yang Diperlukan**  
### 📦 **Daftar Package**  
Berikut adalah daftar package yang diperlukan untuk menjalankan analisis:  
 `requests`   `pandas`   `numpy`   `matplotlib`   `seaborn`   `plotly` 
 `scikit-learn`  

### 💡 *Tips:* Jika belum terinstal, gunakan perintah berikut:  
```bash
!pip install pandas numpy matplotlib seaborn plotly
```

---

## **Bab 3: Eksplorasi Data dan Pembersihan Dataset**  

### 📊 **Dataset yang Digunakan**  
Dataset diambil dari [ScienceDirect](https://www.sciencedirect.com/science/article/pii/S2352340918315191#f0010), mencakup data pemesanan hotel antara 2015 hingga 2017. Dataset berisi 32 variabel, termasuk detail pemesanan, data tamu, serta faktor-faktor yang memengaruhi status reservasi.

### ✨ **Pembersihan Data**  
Setelah menangani nilai NULL, data bersih terdiri dari 118.898 baris. Berikut adalah beberapa langkah yang dilakukan:  
- **Menghapus kolom** dengan nilai NULL yang tidak signifikan (contoh: `country`, `children`).  
- **Mengganti nilai NULL** pada kolom `agent` dan `company` dengan indikator khusus (1000: Tanpa Agen/Perusahaan).  

### 📄 **Ringkasan Pembersihan Data**  
| Variabel       | Nilai Null (Sebelum) | Nilai Null (Sesudah) |  
|----------------|----------------------|----------------------|  
| `children`     | 4                    | 0                    |  
| `country`      | 488                  | 0                    |  

---

## **Bab 4: Exploratory Data Analysis (EDA)**  

### **🔁 Analisis Dasar**  
| **Status Pemesanan** | **Jumlah**  |  
|-----------------------|-------------|  
| Tidak Dibatalkan (0)  | 74,745      |  
| Dibatalkan (1)        | 44,153      |  

Tabel di atas menunjukkan distribusi status pembatalan pemesanan hotel dari tahun 2015 hingga 2017. Dari tabel ini, terlihat bahwa jumlah pemesanan yang tidak dibatalkan (kategori 0) jauh lebih tinggi dibandingkan dengan pemesanan yang dibatalkan (kategori 1). Secara keseluruhan, terdapat lebih dari 70.000 pemesanan yang berhasil terlaksana, sementara pembatalan hanya terjadi pada sekitar 40.000 pemesanan. Perbedaan ini menunjukkan bahwa meskipun pembatalan menjadi masalah signifikan, sebagian besar tamu tetap melanjutkan reservasi mereka, memberikan peluang untuk lebih memahami pola dan faktor yang memengaruhi pembatalan tersebut.  

---

### **🔎 Pola Pemesanan Berdasarkan Asal Tamu**  
#### 🌍 **10 Negara Teratas Asal Tamu:**  
Antara tahun 2015 hingga 2017, mayoritas tamu berasal dari Portugal (PRT) dengan lebih dari 20.000 kunjungan tanpa pembatalan, diikuti oleh Inggris (GBR) dan Prancis (FRA). Selain itu, mayoritas tamu secara keseluruhan berasal dari kategori dewasa (adults) dengan jumlah 136,965, sementara kategori anak-anak (children) dan bayi (babies) memiliki kontribusi yang jauh lebih kecil. Data ini mencerminkan bahwa perjalanan wisata didominasi oleh orang dewasa, dengan Portugal sebagai negara asal tamu terbesar, kemungkinan karena faktor geografis, budaya, dan aksesibilitas.

---

### **🏨 Kategori Tamu Berdasarkan Jenis**  
Dari tabel ini, terlihat bahwa kategori tamu Personal memiliki jumlah pemesanan yang jauh lebih tinggi dibandingkan Company, namun juga lebih banyak mengalami pembatalan. Hal ini menunjukkan bahwa tamu personal lebih mendominasi pasar, mungkin karena mereka lebih fleksibel dalam membuat keputusan perjalanan, sementara tamu dari Company cenderung memiliki rencana yang lebih terstruktur dan jarang membatalkan pemesanan.  

Tamu dari kategori Personal dominan pada tipe pelanggan Transient dan Transient-Party, mencerminkan pemesanan fleksibel oleh individu atau kelompok kecil. Sebaliknya, tamu Company lebih sering terkait dengan tipe pelanggan Contract, karena sifat pemesanan yang terencana. Tipe Group, meski paling sedikit, mencakup tamu Personal dan Company, namun lebih terorganisir dan spesifik. Pola ini menunjukkan hubungan erat antara tujuan perjalanan dan preferensi pemesanan.

---

## **Bab 5: Analisis Lanjutan**  

### **Durasi Menginap Berdasarkan Tipe Pelanggan**  
Visualisasi ini menunjukkan rata-rata durasi menginap (dalam malam) berdasarkan tipe pelanggan dan jenis hotel untuk pemesanan yang tidak dibatalkan. Pelanggan Contract memiliki rata-rata durasi menginap tertinggi, terutama di Resort Hotel dengan rata-rata sekitar 10 malam, diikuti oleh City Hotel dengan durasi lebih pendek. Pelanggan Group dan Transient memiliki rata-rata durasi yang lebih rendah, dengan sebagian besar waktu dihabiskan di Resort Hotel dibandingkan City Hotel. Pelanggan Transient-Party memiliki durasi menginap paling singkat di kedua jenis hotel. Data ini mencerminkan bahwa pelanggan tipe Contract cenderung memesan untuk jangka waktu lebih lama, kemungkinan untuk keperluan kerja atau acara tertentu, sementara pelanggan tipe lainnya cenderung memesan untuk perjalanan yang lebih singkat, terutama di City Hotel.

### **🏦 Tipe Hotel dan Pola Pembatalan**  
Visualisasi ini mengungkap pola pembatalan reservasi pada dua tipe hotel, yaitu City Hotel dan Resort Hotel, dengan kategori status reservasi Not Canceled dan Canceled. Pada City Hotel, jumlah pembatalan cukup tinggi meskipun reservasi yang tidak dibatalkan tetap mendominasi, yang dapat mengindikasikan tantangan dalam mempertahankan komitmen pelanggan. Sebaliknya, Resort Hotel menunjukkan tingkat pembatalan yang lebih rendah secara absolut, meskipun reservasi yang tidak dibatalkan juga lebih tinggi. Temuan ini memberikan indikasi bahwa City Hotel mungkin memerlukan strategi khusus untuk mengurangi pembatalan, seperti peningkatan pengalaman pelanggan atau pengelolaan ekspektasi, sementara Resort Hotel tampak lebih efektif dalam mempertahankan reservasi.

### **🌟 Feature Importance**  
| Rank | Fitur                        | Kepentingan (%) |  
|------|------------------------------|-----------------|  
| 1    | ADR (Average Daily Rate)     | 29.5            |  
| 2    | Lead Time                    | 28.9            |  
| 3    | Deposit Type (Non Refund)    | 14.5            |  
| 4    | Total Special Requests       | 6.2             |  
| 5    | Previous Cancellations       | 5.1             |  

### **Analisis Feature Importance**  
Untuk mendukung analisis ini, berikut disajikan tabel dan visualisasi *feature importance* yang menunjukkan kontribusi masing-masing fitur terhadap model prediksi. Tabel memberikan rincian numerik tentang tingkat pengaruh setiap fitur, sementara grafik batang memvisualisasikan peringkat fitur untuk memudahkan interpretasi.

#### **Analisis Lanjutan pada Feature Penting**
- **Deposit Type (Non Refund):** Kebijakan deposit tanpa pengembalian berhubungan erat dengan pembatalan, kemungkinan akibat kurangnya fleksibilitas yang dirasakan pelanggan.
- **Total Special Requests:** Semakin banyak permintaan khusus yang diajukan, semakin kecil kemungkinan pembatalan, mencerminkan keterlibatan pelanggan yang lebih tinggi.

Visualisasi pertama menunjukkan bahwa mayoritas pelanggan memilih pemesanan tanpa memberikan deposit (No Deposit), sementara visualisasi kedua mengungkapkan bahwa tipe ini memiliki tingkat pembatalan yang signifikan meskipun sebagian besar reservasi tetap dilanjutkan. Sebaliknya, pada tipe Non Refund, pembatalan jauh lebih rendah, yang mencerminkan pengaruh kebijakan deposit terhadap komitmen pelanggan. Untuk mengatasi tingginya tingkat pembatalan pada No Deposit, hotel dapat menawarkan insentif pada opsi Non Refund, seperti diskon harga atau layanan tambahan, guna meningkatkan daya tariknya. Selain itu, pengenalan kebijakan hybrid, seperti deposit sebagian dengan pengembalian sebagian, dapat menyeimbangkan kebutuhan fleksibilitas pelanggan dengan pengurangan pembatalan.

Untuk fitur Total Special Requests, pelanggan dengan **0 permintaan khusus** memiliki tingkat pembatalan tertinggi, sementara semakin banyak permintaan khusus yang diajukan, tingkat pembatalan cenderung menurun. Hal ini mengindikasikan bahwa pengelolaan permintaan khusus dapat menjadi strategi penting dalam meningkatkan komitmen pelanggan. Hotel dapat mendorong keterlibatan pelanggan melalui komunikasi proaktif selama pemesanan, meningkatkan personalisasi layanan, dan memastikan sistem hotel mampu mencatat serta memenuhi permintaan ini secara efisien.

---

## **Bab 6: Kesimpulan dan Rekomendasi**  

### ✍️ **Kesimpulan Utama:**  
Pembatalan reservasi hotel merupakan masalah signifikan yang berdampak pada pendapatan dan efisiensi operasional, terutama pada kategori pemesanan tertentu. Penelitian ini menggunakan dataset pemesanan hotel tahun 2015-2017 dengan 32 variabel, memanfaatkan metodologi Exploratory Data Analysis (EDA) dan Random Forest Classifier untuk memahami pola data dan mengidentifikasi faktor-faktor utama yang memengaruhi pembatalan, seperti deposit_type, total_of_special_requests, ADR, dan lead_time. Analisis menemukan bahwa mayoritas pembatalan terjadi pada pemesanan tanpa deposit (No Deposit), sementara deposit_type Non Refund memiliki tingkat pembatalan jauh lebih rendah. Selain itu, pelanggan dengan 0 permintaan khusus memiliki tingkat pembatalan tertinggi, sedangkan semakin banyak permintaan khusus diajukan, pembatalan cenderung menurun. Puncak pemesanan terjadi pada bulan liburan seperti Agustus, dengan tingkat pembatalan yang lebih tinggi di City Hotel dibandingkan Resort Hotel. Implikasi analisis ini mendorong hotel untuk mengadopsi kebijakan Non Refund dengan insentif, meningkatkan keterlibatan pelanggan melalui permintaan khusus, dan mengoptimalkan pengalaman di City Hotel untuk menurunkan pembatalan. Namun, analisis ini terbatas pada data historis 2015-2017 dan tidak mencakup faktor eksternal seperti kondisi ekonomi atau persaingan industri. Untuk pengembangan lebih lanjut, analisis dapat mencakup data real-time, ulasan pelanggan, atau faktor eksternal guna memberikan wawasan yang lebih relevan dan strategis.

### 💼 **Rekomendasi:**  
1. Tingkatkan pengalaman pelanggan di **City Hotel** untuk mengurangi pembatalan.  
2. Dorong kebijakan **deposit fleksibel** dengan diskon atau layanan tambahan.  
3. Fasilitasi lebih banyak **permintaan khusus** untuk meningkatkan keterlibatan pelanggan.  

---

### ✨ **Acknowledgment:**  
Visualisasi dan analisis dibuat berdasarkan data dari [ScienceDirect](https://www.sciencedirect.com/science/article/pii/S2352340918315191#f0010) dan kode tersedia di [Colab Notebook](https://colab.research.google.com/).

