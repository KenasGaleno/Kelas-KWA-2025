# Soal 3 – Login Bender

## 1. Pendahuluan
Challenge *Login Bender* termasuk kategori **Injection** dengan tingkat kesulitan ⭐⭐⭐ (3/6).  
Tujuannya adalah melakukan login ke akun **bender@juice-sh.op** tanpa mengetahui password aslinya dengan memanfaatkan celah SQL Injection pada form login.

## 2. Identifikasi Titik Injeksi
Petunjuk keberadaan akun Bender dapat ditemukan pada halaman **About → Customer Feedback**, yang menampilkan clue berupa:
Nothing useful available here! (***der@juice-sh.op)

Form ini meminta input `email` dan `password`.

## 3. Penyusunan Payload
Agar bisa login tanpa password, query SQL perlu dimanipulasi supaya kondisi password diabaikan.  

<img width="975" height="493" alt="image" src="https://github.com/user-attachments/assets/af2e2521-8c89-4b42-aef5-2774f1f9e8af" />


Payload pada field email:
```sql
bender@juice-sh.op'--
```

## 4. Eksploitasi

Buka halaman login Juice Shop.

Masukkan payload di kolom email:

bender@juice-sh.op'--

<img width="975" height="492" alt="image" src="https://github.com/user-attachments/assets/c5856a66-19be-4d29-b730-2c3dbb7abbe2" />


dan password bebas.

Kirim request login.

Aplikasi mengembalikan token JWT untuk user bender@juice-sh.op

<img width="1918" height="971" alt="image" src="https://github.com/user-attachments/assets/e0541d46-8319-48b4-a6d0-a5206e6f9f74" />

.

Setelah login, scoreboard menandai challenge Login Bender berhasil
