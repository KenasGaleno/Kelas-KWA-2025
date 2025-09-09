# Soal 2 – Login Jim

## 1. Pendahuluan
Challenge *Login Jim* termasuk kategori **Injection** dengan tingkat kesulitan ⭐⭐⭐.  
Tujuannya adalah melakukan login ke akun **jim@juice-sh.op** tanpa mengetahui password asli dengan memanfaatkan SQL Injection pada form login.

## 2. Identifikasi Titik Injeksi
Petunjuk email Jim dapat ditemukan di halaman **About → Customer Feedback**, yang menampilkan clue seperti:
jim@juice-sh.op

<img width="975" height="492" alt="image" src="https://github.com/user-attachments/assets/d80a4ecf-9634-46f2-949d-8a9379fb12c7" />

Target challenge adalah form **Login** dengan endpoint:
POST /rest/user/login


Form ini menerima input `email` dan `password`.

## 3. Penyusunan Payload
Untuk melewati autentikasi, query SQL perlu dimodifikasi agar password diabaikan.  

Payload:
- **Email:**
  ```sql
  jim@juice-sh.op'--
```
```
## 4. Eksploitasi

Buka halaman login Juice Shop.

Masukkan payload pada field email:

jim@juice-sh.op'--

<img width="975" height="489" alt="image" src="https://github.com/user-attachments/assets/b0f7c8fa-1766-44de-aff4-483186a2a03a" />

dan isi password bebas.

Kirim request login.

Aplikasi mengembalikan token JWT untuk user jim@juice-sh.op

Setelah login, scoreboard menandai challenge Login Jim berhasil

<img width="975" height="492" alt="image" src="https://github.com/user-attachments/assets/2a27f97b-c685-4038-99d8-f30edbc5d4a1" />

<img width="540" height="276" alt="image" src="https://github.com/user-attachments/assets/0f9f2f41-1a9e-4c94-b85b-f3745f54cf99" />

