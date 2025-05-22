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

Melalui pendekatan **Exploratory Data Analysis (EDA)**, project ini bertujuan untuk mengeksplorasi data transaksi pemesanan secara komprehensif dari sisi **waktu, lokasi, kategori produk, serta performa pengiriman**, sehingga dapat ditemukan pola-pola penting yang dapat dijadikan dasar dalam pembuatan strategi bisnis yang lebih baik.

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

---

### **Contoh Data**

| store\_code | store\_location     | order\_id           | user\_id | order\_time | delivered\_time | products\_persona\_agg  | user\_location       | total\_value\_order |
| ----------- | ------------------- | ------------------- | -------- | ----------- | --------------- | ----------------------- | -------------------- | ------------------- |
| 10011       | -6.168783,106.87677 | App-7001192545-1-01 | 1697711  | 1.71125E+12 | 1.71126E+12     | fresh,sembako           | -6.1522268,106.83874 | 100350              |
| 10011       | -6.168783,106.87677 | App-7001121785-1-01 | 1440401  | 1.71014E+12 | (null)          | household,sembako,snack | -6.1303084,106.85455 | 251420              |



