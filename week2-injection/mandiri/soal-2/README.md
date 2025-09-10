# Soal Mandiri 2 
# SQL Injection Vulnerability Allowing Login Bypass

Lab ini memiliki celah **SQL Injection** pada fungsi login.  
Tujuannya adalah login sebagai user **administrator** tanpa mengetahui password.


![WhatsApp Image 2025-09-10 at 17 42 18_d078b377](https://github.com/user-attachments/assets/d065cc5e-503d-462f-87df-2bd9269e23d3)


## 2. Link Resource
- [Lab: SQL injection vulnerability allowing login bypass](https://portswigger.net/web-security/sql-injection/lab-login-bypass)
- [Referensi: SQL Injection – PortSwigger Academy](https://portswigger.net/web-security/sql-injection)

## 3. Langkah Pengerjaan

### 🔹 Step 1 – Akses Login Form
Buka halaman login lab.  
Form meminta **username** dan **password**.

<img width="1452" height="738" alt="image" src="https://github.com/user-attachments/assets/aae21bf5-110d-4c23-9e51-828ab5c137de" />

### 🔹 Step 2 – Intercept dengan Burp Suite
Request login berhasil ditangkap oleh Burp Proxy.  
Metode: `POST /login` dengan parameter `username` dan `password`.

<img width="1382" height="732" alt="image" src="https://github.com/user-attachments/assets/e6c5e217-556f-4e42-b9ff-4ed67cfd21c0" />

### 🔹 Step 3 – Kirim ke Repeater
Request dipindahkan ke **Repeater** untuk diuji payload.  

<img width="1387" height="737" alt="image" src="https://github.com/user-attachments/assets/3edb36d3-d8fc-434c-b1fe-e5d784f6cab5" />

<img width="1391" height="738" alt="image" src="https://github.com/user-attachments/assets/02753f41-bd4b-4027-b0a8-f472cdd7ee48" />

### 🔹 Step 4 – Tambahkan Payload SQL Injection
Masukkan payload berikut ke parameter **username**:

<img width="1467" height="737" alt="image" src="https://github.com/user-attachments/assets/cc61d818-9075-48da-9fed-ce7db5ff6afb" />

<img width="1462" height="737" alt="image" src="https://github.com/user-attachments/assets/c142be57-8b20-4e88-951c-af9ad61853fe" />



