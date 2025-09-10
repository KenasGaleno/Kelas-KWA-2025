# Soal Mandiri 3 
SQL Injection Attack – Listing Database Contents (Non-Oracle)
1. Identifikasi Target
<img width="975" height="487" alt="image" src="https://github.com/user-attachments/assets/c1ec3ca4-b90d-4a6a-8dfc-560cdd8c7478" />

Endpoint rentan:

GET /filter?category=Pets
<img width="975" height="512" alt="image" src="https://github.com/user-attachments/assets/feeb3ad1-363a-42d2-a77d-fd2f4a4008b9" />


Parameter category menerima input langsung tanpa sanitasi, sehingga rawan SQL Injection.

2. Uji Kerentanan

Awalnya diuji dengan menambahkan tanda ' untuk melihat apakah query error.
Contoh:

/filter?category=Pets'
<img width="975" height="514" alt="image" src="https://github.com/user-attachments/assets/dac17581-c111-4b96-9148-5c037f90c8f7" />


Hasilnya menunjukkan error SQL → menandakan parameter rentan.

3. Menentukan Jumlah Kolom

Dengan metode UNION SELECT NULL, dicoba beberapa variasi hingga menemukan jumlah kolom yang sesuai.
Contoh payload:

/filter?category=Pets' UNION SELECT NULL,NULL--


Jika muncul error, jumlah NULL ditambah hingga sesuai. Dari percobaanmu, jumlah kolom terdeteksi 2.

4. Enumerasi Database

Setelah tahu jumlah kolom, tahap berikutnya adalah menampilkan informasi versi database menggunakan payload:

/filter?category=Pets' UNION SELECT banner, NULL FROM v$version--

<img width="975" height="516" alt="image" src="https://github.com/user-attachments/assets/aa79772e-b658-4436-8e7c-f6e7436a2cdb" />

Namun karena challenge ini adalah non-Oracle, query yang sesuai untuk MySQL/PostgreSQL adalah dengan menargetkan version() atau metadata dari information_schema.

Contoh payload sukses (berdasarkan dokumentasi kamu):

/filter?category=Pets' UNION SELECT banner, NULL FROM v$version--

<img width="975" height="515" alt="image" src="https://github.com/user-attachments/assets/9bf82ade-d6d9-4ec2-a3f8-605f817cfd6f" />

Respons menampilkan string versi database (MySQL / PostgreSQL / lainnya).

<img width="975" height="520" alt="image" src="https://github.com/user-attachments/assets/e594d4a7-ece6-4335-80f2-ecc7ba25acc6" />
