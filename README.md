![Allofresh](https://allofresh.id/blog/wp-content/uploads/2024/02/homebanner_ALLOFRESH-CLUB.png)


## **Project Overview: Analisis Data Pemesanan & Pengiriman Produk allofresh**

### **Overview Project:**

Project ini bertujuan untuk melakukan eksplorasi terhadap data pemesanan dan pengiriman produk allofresh untuk menggali insight tentang pola pembelian, performa pengiriman, kategori produk terpopuler, serta pengaruh lokasi terhadap nilai dan durasi pesanan. Hasil insight ini diharapkan dapat membantu perusahaan dalam pengambilan keputusan strategis seperti:

* Optimalisasi lokasi toko
* Rekomendasi kategori produk
* Perbaikan layanan pengiriman
* Segmentasi pelanggan


## **Latar Belakang:**

Perusahaan retail digital kini menghadapi tantangan dalam mengelola pesanan yang berasal dari berbagai lokasi dengan permintaan yang bervariasi. Kecepatan pengiriman dan preferensi produk menjadi faktor utama dalam menjaga kepuasan pelanggan. Dengan semakin luasnya jangkauan layanan dan beragamnya kategori produk yang ditawarkan, perusahaan memerlukan sistem analisis berbasis data untuk memahami:

* **Perilaku pelanggan:** Apa saja produk yang paling sering dibeli? Siapa pelanggan paling aktif?
* **Kinerja pengiriman:** Seberapa cepat pesanan dikirim? Apakah jarak memengaruhi durasi pengiriman?
* **Efisiensi lokasi toko:** Toko mana yang memiliki cakupan pelanggan paling besar?
* **Nilai transaksi:** Apa saja faktor yang memengaruhi total nilai pesanan?


Melalui pendekatan **Exploratory Data Analysis (EDA)**, proyek ini akan menganalisis data untuk menjawab pertanyaan-pertanyaan kunci ini dan memberikan rekomendasi yang dapat ditindaklanjuti.

-----

### **Pertanyaan Bisnis:**

Project ini akan berfokus pada menjawab pertanyaan-pertanyaan bisnis berikut:

**Pola Pembelian Berdasarkan Waktu:**

1.  Bagaimana korelasi antara waktu pemesanan dengan frekuensi *order*?
2.  Bagaimana distribusi nilai *order* (transaksi) pelanggan Allofresh sepanjang hari (per jam)? Adakah jam-jam tertentu yang menunjukkan nilai *order* rata-rata yang lebih tinggi atau lebih rendah?
3.  Bagaimana distribusi nilai *order* (transaksi) pelanggan Allofresh berdasarkan hari dalam seminggu? Apakah ada perbedaan signifikan antara hari kerja dan akhir pekan dalam hal nilai transaksi atau frekuensi pembelian?

**Kategori Produk Terpopuler dan Nilai Order:**

1.  Kategori produk apa saja yang memiliki rata-rata nilai *order* tertinggi dan terendah?
2.  Kategori produk apa saja yang paling sering di-*order* (frekuensi tertinggi) dan paling jarang di-*order*?
3.  Bagaimana hubungan antara rata-rata nilai *order* dan frekuensi *order* untuk setiap kategori produk? (Misalnya, apakah kategori dengan nilai *order* tinggi cenderung memiliki frekuensi *order* rendah, dan sebaliknya?)

**Performa Pengiriman dan Pengaruh Lokasi:**

1.  Bagaimana performa durasi pengiriman secara keseluruhan (rata-rata, median, distribusi)?
2.  Apakah ada perbedaan durasi pengiriman yang signifikan berdasarkan jarak pengiriman atau wilayah/lokasi pelanggan?

**Perilaku Pengiriman dan Kluster Pelanggan:**

1.  Berapa segmen pelanggan utama yang dapat diidentifikasi berdasarkan pola pembelian mereka (nilai *order*, waktu pemesanan, frekuensi, jarak pengiriman)?
2.  Bagaimana karakteristik masing-masing kluster pelanggan terkait dengan rata-rata nilai *order*, waktu pemesanan, frekuensi, jarak pengiriman?
3.  Bagaimana Allofresh dapat menargetkan setiap segmen ini dengan strategi pemasaran atau promosi yang disesuaikan?

---

## **Data Understanding**

### **Sumber Data**
Berikut informasi pada dataset :
* Dataset dengan format CSV (Comma-Seperated Values)
* Dataset memiliki 40722 record dengan 9 feature
* Dataset memiliki 3 feature numerik dan 6 feature kategori
* Terdapat missing value dalam dataset

Dataset berisi data transaksi pemesanan yang mencakup informasi:
* Lokasi toko dan pengguna
* Waktu pemesanan dan pengiriman
* Kategori produk
* Nilai total pesanan

Data ini bersifat transactional dan direkam secara otomatis dari aplikasi pemesanan.

---

### **Struktur Dataset**

| Kolom                  | Tipe Data                  | Deskripsi                                                            |
| ---------------------- | -------------------------- | -------------------------------------------------------------------- |
| `store_code`           | Integer                    | Kode unik untuk masing-masing toko.                                  |
| `store_location`       | String (koordinat)         | Lokasi toko dalam format `latitude,longitude`.                       |
| `order_id`             | String                     | ID unik setiap transaksi/order.                                      |
| `user_id`              | Integer/String             | ID pengguna yang melakukan order.                                    |
| `order_time`           | Float (timestamp)          | Waktu pemesanan dalam format Unix timestamp (ms).                    |
| `delivered_time`       | Float (timestamp / kosong) | Waktu pengiriman selesai. Kosong jika belum terkirim.                |
| `products_persona_agg` | String                     | Kategori produk yang dipesan (dipisahkan koma jika lebih dari satu). |
| `user_location`        | String (koordinat)         | Lokasi pengguna dalam format `latitude,longitude`.                   |
| `total_value_order`    | Integer                    | Total nilai transaksi (dalam Rupiah).                                |

### **Contoh Data:**

| store\_code | store\_location     | order\_id           | user\_id | order\_time | delivered\_time | products\_persona\_agg  | user\_location       | total\_value\_order |
| :---------- | :------------------ | :------------------ | :------- | :---------- | :-------------- | :---------------------- | :------------------- | :------------------ |
| 10011       | -6.168783,106.87677 | App-7001192545-1-01 | 1697711  | 1.71125E+12 | 1.71126E+12     | fresh,sembako           | -6.1522268,106.83874 | 100350              |
| 10011       | -6.168783,106.87677 | App-7001192545-1-02 | 1697711  | 1.71125E+12 | 1.71126E+12     | fresh                   | -6.1522268,106.83874 | 85000               |
| 10011       | -6.168783,106.87677 | App-7001192545-1-03 | 1697711  | 1.71125E+12 | 1.71126E+12     | fresh,beverage          | -6.1522268,106.83874 | 125000              |
| 10011       | -6.168783,106.87677 | App-7001192545-1-04 | 1697711  | 1.71125E+12 | 1.71126E+12     | daging,ayam,ikan        | -6.1522268,106.83874 | 180000              |
| 10011       | -6.168783,106.87677 | App-7001192545-1-05 | 1697711  | 1.71125E+12 | 1.71126E+12     | sembako                 | -6.1522268,106.83874 | 50000               |

---

## **Tahapan Analisis Data:**

1.  **Pengumpulan Data:** Mengunduh dataset yang relevan.
2.  **Pembersihan Data:**
    * Mengatasi nilai yang hilang (missing values).
    * Mengonversi tipe data yang tidak sesuai (misalnya, timestamp ke format tanggal/waktu yang dapat dibaca).
    * Menangani duplikasi data.
3.  **Rekayasa Fitur (Feature Engineering):**
    * Ekstraksi `order_hour`, `order_day_of_week`, `delivery_duration_minutes`.
    * Penghitungan jarak antara `store_location` dan `user_location`.
    * Pengolahan kolom `products_persona_agg` untuk analisis kategori produk.
4.  **Analisis Eksplorasi Data (EDA):**
    * Visualisasi distribusi variabel kunci.
    * Analisis tren waktu (jam sibuk, hari sibuk).
    * Korelasi antara jarak dan durasi pengiriman.
    * Analisis kategori produk terpopuler dan pola pembelian per toko.
    * Visualisasi persebaran lokasi pelanggan dan toko.
5.  **Segmentasi Pelanggan (Clustering):**
    * Menggunakan algoritma *Clustering* (misalnya, K-Means) untuk mengidentifikasi segmen pelanggan berdasarkan perilaku pembelian (waktu order, nilai order, durasi pengiriman, jarak).
    * Interpretasi dan profiling masing-masing cluster.
6.  **Interpretasi dan Rekomendasi:**
    * Menyajikan *insight* utama dari analisis.
    * Memberikan rekomendasi yang dapat ditindaklanjuti untuk strategi bisnis.

---


## **Hasil dan Insight Utama:**

Berikut adalah beberapa *insight* kunci yang ditemukan selama analisis:

### **1. Pola Pembelian Berdasarkan Waktu:**

* **Korelasi Antara Waktu Pemesanan dengan Frekuensi Order:**
    * **Insight:** Frekuensi *order* menunjukkan korelasi yang jelas dengan waktu pemesanan (jam dalam sehari). Frekuensi *order* memuncak secara signifikan di pagi hari, yaitu antara jam 04:00 hingga 08:00 WIB, dengan puncak tertinggi di sekitar jam 06:00 WIB. Setelah itu, frekuensi menurun drastis hingga siang hari dan mengalami sedikit kenaikan lagi di malam hari (sekitar jam 21:00-23:00 WIB), meskipun tidak setinggi puncak pagi. Frekuensi *order* cenderung meningkat secara signifikan menjelang akhir minggu, dengan puncak tertinggi pada Hari 5 dan Hari 6 (Sabtu dan Minggu). Hari-hari kerja (Hari 0-4) memiliki frekuensi *order* yang lebih stabil dan lebih rendah.
    * **Penjelasan Grafik:** Grafik ini, kemungkinan adalah *line plot* atau *bar chart* yang menunjukkan jumlah *order* per jam dan per hari dalam seminggu. Puncak di pagi hari (04:00-08:00) dan di akhir pekan (Hari 5 & 6) sangat jelas terlihat, mengindikasikan waktu-waktu tersibuk untuk pemesanan.
    * ![Frekuensi Order per Jam dan Hari](https://raw.githubusercontent.com/[YOUR_USERNAME]/[YOUR_REPO_NAME]/main/images/frekuensi_order_per_jam_hari.png)
        Gambar 1. Frekuensi Order berdasarkan Jam dan Hari dalam Seminggu.

* **Distribusi Nilai Order (Transaksi) Pelanggan Allofresh Sepanjang Hari (per Jam):**
    * **Insight:** Distribusi nilai *order* per jam menunjukkan bahwa median nilai *order* cenderung sangat konsisten di sepanjang hari (sekitar Rp 100.000 - Rp 150.000). Tidak ada jam-jam tertentu yang secara signifikan menunjukkan nilai *order* rata-rata (median) yang jauh lebih tinggi atau lebih rendah. Meskipun ada fluktuasi frekuensi *order*, jenis atau nilai pesanan (dari median hingga rentang atas tanpa *outlier*) tidak banyak berubah per jam. Ini mengindikasikan bahwa pelanggan melakukan pembelian dengan nilai yang serupa, terlepas dari jam berapa mereka berbelanja.
    * **Penjelasan Grafik:** Sebuah *box plot* atau *violin plot* yang membandingkan distribusi nilai *order* untuk setiap jam akan menunjukkan median yang stabil. Hal ini menegaskan bahwa meskipun jumlah pesanan bervariasi, ukuran transaksi individu cenderung konstan.
    * ![Distribusi Nilai Order per Jam](https://raw.githubusercontent.com/[YOUR_USERNAME]/[YOUR_REPO_NAME]/main/images/distribusi_nilai_order_per_jam.png)
        Gambar 2. Distribusi Nilai Order per Jam.

* **Distribusi Nilai Order (Transaksi) Pelanggan Allofresh Berdasarkan Hari dalam Seminggu:**
    * **Insight:** Distribusi nilai *order* per jam menunjukkan bahwa median nilai *order* cenderung sangat konsisten di sepanjang minggu. Namun terdapat nilai *order* yang *outlier* di akhir pekan.
    * **Penjelasan Grafik:** Mirip dengan distribusi per jam, *box plot* atau *violin plot* per hari dalam seminggu akan menampilkan median yang stabil antar hari kerja dan akhir pekan. Adanya *outlier* yang lebih banyak di akhir pekan akan terlihat sebagai titik-titik di luar "jangkar" *box plot*, menunjukkan adanya pesanan dengan nilai sangat tinggi pada hari-hari tersebut.
    * ![Distribusi Nilai Order per Hari dalam Seminggu](https://raw.githubusercontent.com/[YOUR_USERNAME]/[YOUR_REPO_NAME]/main/images/distribusi_nilai_order_per_hari.png)
        Gambar 3. Distribusi Nilai Order per Hari dalam Seminggu. 

### **2. Kategori Produk Terpopuler dan Nilai Order:**

* **Kategori Produk dengan Rata-rata Nilai Order Tertinggi dan Terendah:**
    * **Insight:** Rata-rata nilai *order* tertinggi adalah kategori "Other", menunjukkan rata-rata nilai *order* sedikit di atas Rp 200.000. Sedangkan rata-rata nilai *order* terendah adalah kategori "Household", memiliki rata-rata nilai *order* di bawah Rp 100.000 (sekitar Rp 75.000).
    * **Penjelasan Grafik:** Sebuah *bar chart* yang menampilkan rata-rata nilai `total_value_order` untuk setiap `products_persona_agg` akan dengan jelas menunjukkan perbedaan antara kategori "Other" sebagai yang tertinggi dan "Household" sebagai yang terendah.
    * ![Rata-rata Nilai Order per Kategori Produk](https://raw.githubusercontent.com/[YOUR_USERNAME]/[YOUR_REPO_NAME]/main/images/rata_rata_nilai_order_per_kategori.png)
        Gambar 4. Rata-rata Nilai Order per Kategori Produk. 

* **Kategori Produk Paling Sering Diorder (Frekuensi Tertinggi) dan Paling Jarang Diorder:**
    * **Insight:** Berdasarkan analisis frekuensi *order* per kategori produk, terlihat bahwa "sembako" mendominasi daftar teratas sebagai kategori yang paling sering di-*order*, dengan jumlah transaksi yang melampaui 20.000 *order*. Hal ini mengindikasikan bahwa produk kebutuhan pokok merupakan pilar utama volume transaksi bagi bisnis ini, mencerminkan kebutuhan dasar yang sering dipenuhi oleh pelanggan. Di sisi lain, kategori "other" menempati posisi paling bawah dalam hal frekuensi *order*, bahkan hampir tidak terlihat di grafik. Kategori ini diikuti oleh "household" dan "fresh" yang juga menunjukkan frekuensi *order* yang relatif rendah, berkisar antara 4.000 hingga 5.000 *order*. Pola ini menyoroti fokus utama pelanggan pada kebutuhan harian esensial dibandingkan pembelian barang-barang yang mungkin lebih spesifik atau kurang sering dibutuhkan.
    * **Penjelasan Grafik:** Sebuah *bar chart* yang menunjukkan hitungan (`count`) dari setiap `products_persona_agg` akan memvisualisasikan dominasi "sembako" dan rendahnya frekuensi "other", "household", dan "fresh".
    * ![Frekuensi Order per Kategori Produk](https://raw.githubusercontent.com/[YOUR_USERNAME]/[YOUR_REPO_NAME]/main/images/frekuensi_order_per_kategori.png)
        Gambar 5. Frekuensi Order per Kategori Produk. 

* **Hubungan Antara Rata-rata Nilai Order dan Frekuensi Order untuk Setiap Kategori Produk:**
    * **Insight:** Terdapat hubungan terbalik yang terlihat jelas antara kategori "other" (nilai *order* tinggi, frekuensi sangat rendah) dan "sembako" (frekuensi sangat tinggi, nilai *order* moderat). Ini menunjukkan bahwa pelanggan cenderung membeli kebutuhan pokok (sembako) dalam jumlah sering dengan nilai transaksi yang tidak terlalu besar per pembelian, sementara pembelian barang dari kategori "other" mungkin lebih jarang namun bernilai tinggi. Kategori "fresh" cenderung rendah di kedua aspek (nilai rata-rata dan frekuensi).
    * **Penjelasan Grafik:** Sebuah *scatter plot* dengan frekuensi *order* pada sumbu X dan rata-rata nilai *order* pada sumbu Y, dengan label untuk setiap kategori produk, akan secara visual menampilkan posisi relatif setiap kategori dan hubungan terbalik yang dijelaskan.
    * ![Hubungan Nilai vs Frekuensi Order per Kategori](https://raw.githubusercontent.com/[YOUR_USERNAME]/[YOUR_REPO_NAME]/main/images/hubungan_nilai_frekuensi_kategori.png)
        Gambar 6. Hubungan Rata-rata Nilai Order dan Frekuensi Order per Kategori Produk.

### **3. Performa Pengiriman dan Pengaruh Lokasi:**

* **Performa Durasi Pengiriman Keseluruhan (Rata-rata, Median, Distribusi):**
    * **Insight:** Durasi pengiriman rata-rata adalah sekitar 4.43 jam. Distribusi durasi pengiriman miring ke kanan (*positively skewed*). Ini berarti sebagian besar pengiriman diselesaikan dalam waktu yang relatif singkat (di bawah 5 jam), namun ada juga pengiriman yang memakan waktu lebih lama.
    * **Penjelasan Grafik:** Sebuah histogram atau *density plot* dari kolom `delivery_duration_hours` akan menunjukkan bentuk distribusi yang miring ke kanan, dengan puncak di sekitar 4-5 jam dan ekor panjang ke arah durasi yang lebih lama.
    * ![Distribusi Durasi Pengiriman](https://raw.githubusercontent.com/[YOUR_USERNAME]/[YOUR_REPO_NAME]/main/images/distribusi_durasi_pengiriman.png)
        Gambar 7. Distribusi Durasi Pengiriman. 

* **Perbedaan Durasi Pengiriman Berdasarkan Jarak Pengiriman atau Wilayah/Lokasi Pelanggan:**
    * **Insight:** Grafik "Delivery Duration vs Distance" menunjukkan korelasi positif yang jelas antara jarak pengiriman dan durasi pengiriman. Semakin jauh jaraknya, durasi pengiriman cenderung semakin lama. Namun, ada variabilitas yang signifikan; untuk jarak yang sama, durasi pengiriman bisa sangat bervariasi, menunjukkan faktor lain ikut berperan seperti kepadatan lalu lintas yang lebih tinggi di kota-kota padat seperti di Jakarta.
    * **Penjelasan Grafik:** *Scatter plot* dengan `delivery_distance_km` pada sumbu X dan `delivery_duration_hours` pada sumbu Y akan menunjukkan pola titik-titik yang naik dari kiri bawah ke kanan atas, mengonfirmasi korelasi positif. Namun, penyebaran titik-titik di sekitar tren menunjukkan variabilitas yang disebabkan oleh faktor-faktor lain.
    * ![Durasi Pengiriman vs Jarak](https://raw.githubusercontent.com/[YOUR_USERNAME]/[YOUR_REPO_NAME]/main/images/durasi_pengiriman_vs_jarak.png)
        Gambar 8. Durasi Pengiriman vs Jarak. 

### **4. Perilaku Pengiriman dan Kluster Pelanggan:**

* **Identifikasi Segmen Pelanggan Utama:**
    * **Insight:** Berdasarkan analisis klaster (menggunakan K-Means), Allofresh dapat mengidentifikasi tiga segmen pelanggan utama.

* **Karakteristik Masing-masing Kluster Pelanggan:**
    * **Cluster 0 (Pelanggan Malam Hari - Menengah):**
        * **Karakteristik:** Pelanggan ini cenderung memesan pada malam hari (sekitar pukul 18.30) dengan nilai *order* menengah. Jarak pengirimannya sedang.
        * **Insight:** Mereka kemungkinan adalah pekerja atau keluarga yang beraktivitas di siang hari dan baru sempat berbelanja setelah jam kerja.
        * **Penjelasan Profil:** Profil *cluster* ini akan ditunjukkan melalui nilai rata-rata atau median dari fitur-fitur yang digunakan dalam *clustering* (`order_hour`, `total_value_order`, `delivery_distance_km`, `order_day_of_week`) untuk *cluster* 0, yang dapat divisualisasikan dalam *bar plot* karakteristik *cluster*.
    * **Cluster 1 (Pelanggan Pagi Hari - Rutin/Kecil):**
        * **Karakteristik:** Ini adalah kluster terbesar, dengan pelanggan yang memesan pada pagi hari (sekitar pukul 06.30) dengan jarak pengiriman paling dekat dan nilai *order* paling rendah.
        * **Insight:** Mereka mewakili pembeli rutin harian, seperti rumah tangga yang berbelanja kebutuhan pokok.
        * **Penjelasan Profil:** Profil *cluster* ini akan ditunjukkan melalui nilai rata-rata atau median dari fitur-fitur yang sama untuk *cluster* 1.
    * **Cluster 2 (Pelanggan Pagi Hari - Besar/Volume Tinggi):**
        * **Karakteristik:** Segmen ini memiliki nilai *order* tertinggi (rata-rata sekitar Rp 299.000) dan juga memesan pada pagi hari. Jarak pengirimannya sedang.
        * **Insight:** Kluster ini kemungkinan besar terdiri dari pelanggan yang melakukan pembelian dalam jumlah besar, seperti untuk stok bulanan atau keperluan bisnis kecil.
        * **Penjelasan Profil:** Profil *cluster* ini akan ditunjukkan melalui nilai rata-rata atau median dari fitur-fitur yang sama untuk *cluster* 2.
    * ![Profil Karakteristik Cluster Pelanggan](https://raw.githubusercontent.com/[YOUR_USERNAME]/[YOUR_REPO_NAME]/main/images/profil_cluster_pelanggan.png)
        Gambar 10. Profil Karakteristik Setiap Cluster Pelanggan. 

---

## **Rekomendasi Strategis:**

Berdasarkan *insight* yang diperoleh, berikut adalah rekomendasi strategis untuk Allofresh:

### **1. Optimalisasi Pemasaran Berdasarkan Segmen Pelanggan:**

* **Cluster 0 (Pelanggan Malam Hari - Menengah):** Allofresh dapat menargetkan segmen ini dengan promosi "makan malam cepat" atau diskon untuk produk-produk yang sering dibeli di sore hari. Personalisasi penawaran berdasarkan riwayat pembelian di malam hari juga bisa efektif.
* **Cluster 1 (Pelanggan Pagi Hari - Rutin/Kecil):** Fokus pada program loyalitas, langganan produk rutin, atau penawaran *bundling* untuk kebutuhan sehari-hari. Promosi di pagi hari atau "flash sale" untuk produk segar dapat menarik segmen ini.
* **Cluster 2 (Pelanggan Pagi Hari - Besar/Volume Tinggi):** Menawarkan diskon pembelian dalam jumlah besar, program keanggotaan premium dengan keuntungan pengiriman gratis atau prioritas, dan penawaran khusus untuk produk-produk premium atau kategori "Daging dan Seafood". Membangun hubungan B2B dengan usaha kecil juga bisa menjadi strategi.

### **2. Peningkatan Efisiensi Pengiriman:**

* **Analisis Rute:** Gunakan data jarak dan durasi pengiriman untuk mengoptimalkan rute pengiriman, terutama di jam sibuk pagi dan malam hari.
* **Manajemen Jam Sibuk:** Alokasikan lebih banyak *driver* atau sumber daya di jam puncak pemesanan (pagi hari, khususnya pukul 04:00-08:00, dan akhir pekan) untuk memastikan durasi pengiriman tetap optimal.
* **Umpan Balik Pelanggan:** Kumpulkan umpan balik mengenai durasi pengiriman untuk terus melakukan perbaikan.

### **3. Strategi Produk & Inventaris:**

* **Penyesuaian Stok:** Pastikan ketersediaan produk `sembako` selalu terjaga karena frekuensi *order* yang sangat tinggi.
* **Promosi Berbasis Kategori:** Pertimbangkan promosi untuk kategori "Other" yang memiliki nilai *order* tinggi namun frekuensi rendah untuk mendorong pembelian yang lebih sering.
* **Peningkatan Kategori Rendah Frekuensi:** Evaluasi strategi untuk kategori "household" dan "fresh" yang memiliki frekuensi *order* rendah, mungkin dengan penawaran *bundling* atau promosi silang.

### **4. Optimalisasi Lokasi Toko:**

* Lakukan analisis lebih lanjut mengenai lokasi toko dan jangkauan pelanggan untuk mengidentifikasi area yang belum terlayani secara optimal atau berpotensi tinggi untuk pembukaan toko baru, khususnya di daerah perkotaan padat penduduk.
* Pertimbangkan model "dark store" atau *fulfillment center* di area dengan kepadatan pelanggan tinggi namun belum terjangkau oleh toko fisik.

---


