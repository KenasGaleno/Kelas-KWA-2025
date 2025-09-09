# Soal 1 – Login Admin

## 1. Pendahuluan
Challenge *Login Admin* termasuk kategori **Injection** dengan tingkat kesulitan ⭐⭐.  
Tujuannya adalah melakukan login ke akun administrator (`admin@juice-sh.op`) tanpa mengetahui password sebenarnya dengan memanfaatkan celah SQL Injection.

## 2. Identifikasi Titik Injeksi
Target challenge adalah form **Login** pada aplikasi OWASP Juice Shop.  
Endpoint yang digunakan:
POST /rest/user/login


Form ini menerima input `email` dan `password`.  

input `'` pada field `email` atau `password` menghasilkan error, menandakan adanya SQL Injection.

<img width="975" height="493" alt="image" src="https://github.com/user-attachments/assets/d2b6e5a6-db85-4b2b-b455-4938cd163007" />

## 3. Penyusunan Payload
Untuk mem-bypass login dan masuk sebagai admin, digunakan payload SQL Injection sederhana.

- **Payload 1:**
  ```sql
  ' OR true--
  ```

  ## 4. Eksploitasi

Buka halaman login Juice Shop.

Masukkan payload ' OR true -- di kolom email, isi password sembarang (misalnya 1234).

Klik login.

<img width="975" height="492" alt="image" src="https://github.com/user-attachments/assets/33e02f64-91b2-43c7-8807-e1b22e5f2961" />

Aplikasi memberikan token JWT untuk user admin@juice-sh.op

Scoreboard menandai challenge Login Admin berhasil

<img width="975" height="492" alt="image" src="https://github.com/user-attachments/assets/eb7f33a0-6c01-4a4b-aa2b-1536cfb276fc" />

<img width="436" height="221" alt="image" src="https://github.com/user-attachments/assets/362fa501-92d5-47a8-b920-a689c041eefa" />

