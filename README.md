# Technical_Test_intren

**1. WITH monthly_orders_product AS (...):** Membuat temporary table untuk mengelompokkan data berdasarkan bulan (created_at) product_id, product_category, product_name, dan product_brand menghitung total order (COUNT(id)) dan total retail (SUM(product_retail_price)) per produk.


**2. FORMAT_TIMESTAMP('%Y-%m', created_at):** Mengubah tanggal created_at menjadi format tahun-bulan (contoh: 2025-04), sehingga kita bisa agregasi per bulan.


**3. COUNT(id) AS total_orders**: Menghitung jumlah transaksi/order untuk produk tersebut di bulan itu.


**4. SUM(product_retail_price) AS total_retail:** Menjumlahkan nilai penjualan dari produk itu di bulan tersebut.


**5. FROM `bigquery-public-data.thelook_ecommerce.inventory_items:** Query ini mengakses data dari tabel **inventory_items** yang berada dalam dataset thelook_ecommerce yang merupakan bagian dari bigquery-public-data, sebuah koleksi dataset publik yang disediakan oleh Google BigQuery.


**6. WHERE:** Diguankan untuk memfiltir. Mengekstrak data yang memenuhi kondisi tertentu


**7. GROUPP BY:** Mengelompokan baris-baris 


**8. ROW_NUMBER() OVER (PARTITION BY created_at ORDER BY total_orders DESC) AS rank_order:** Membagi data berdasarkan created_at (bulan). Lalu mengurutkan per bulan berdasarkan total_orders (jumlah order) dari yang terbanyak ke terkecil.


**9. ROW_NUMBER():** Memberi nomor urut mulai dari 1. Jadi setiap bulan, produk dengan order terbanyak akan punya rank_order = 1.


**10. ORDER BY total_retail DESC:** Mengammbil produk top 1 per bulan, hasilnya diurutkan dari yang total penjualannya paling besar.


**11. ORDER BY total_orders:** Mengammbil produk top 1 per bulan, hasilnya diurutkan dari yang total order paling banyak.

**11. LIMIT 10:** Batsan ini menentukan bahwa hanya 10 produk dengan nilai total_retail terbesar di antara semua top 1 produk per bulan. Ini berguna untuk membatasi jumlah data yang diambil, yang bisa sangat membantu ketika bekerja dengan set data besar atau ketika hanya ingin melihat contoh data untuk pemahaman awal struktur dan isi tabel.
