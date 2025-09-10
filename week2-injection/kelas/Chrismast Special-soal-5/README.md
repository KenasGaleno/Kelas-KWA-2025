# Soal 5 – Christmas Special

## 1. Pendahuluan
Challenge *Christmas Special* termasuk kategori **Injection** dengan tingkat kesulitan ⭐⭐⭐⭐.  
Tujuannya adalah memanfaatkan celah SQL Injection pada fitur pencarian produk untuk menemukan dan menambahkan produk tersembunyi bernama **Christmas Special (2014 Edition)** ke keranjang belanja.

## 2. Identifikasi Titik Injeksi
Eksperimen dilakukan pada **Juice Shop** yang dijalankan lokal melalui Docker:http://127.0.0.1:3000/rest/products/search?q=
<payload>
<img width="975" height="443" alt="image" src="https://github.com/user-attachments/assets/fa294429-460f-4058-8e31-dd95dce88d0c" />

Parameter `q` pada fitur pencarian diuji dengan tanda `'`.  

## 3. Menentukan Payload
Uji coba `UNION SELECT` digunakan untuk memanipulasi query asli.  
Tujuannya adalah menampilkan produk yang statusnya *deleted* atau tersembunyi. 

<img width="975" height="440" alt="image" src="https://github.com/user-attachments/assets/2dc26263-d1d7-44a8-8d7f-09438f5e75a9" />


4. Eksploitasi

Berdasarkan urutan pengerjaan:

Uji SQL Injection di search

Memasukkan payload ke parameter q.

Hasilnya JSON berisi daftar produk, termasuk item tersembunyi.

Verifikasi hasil di DevTools

Pada tab Network, response search?q= memperlihatkan produk Christmas Special.

Data JSON memuat detail seperti id, name, description, dan harga.

Tambahkan ke keranjang

Menggunakan endpoint /api/BasketItems/ dengan request body:

{
  "ProductId": 30,
  "BasketId": "6",
  "quantity": 1
}


Request berhasil (status: success).

Cek isi keranjang

Produk Christmas Super-Surprise-Box (2014 Edition) muncul di basket.

Total harga keranjang bertambah sesuai harga produk.

📌 Bukti visual:

<img width="975" height="496" alt="image" src="https://github.com/user-attachments/assets/d3ffc790-73f1-4449-b9e7-7c2683348002" />
<img width="975" height="579" alt="image" src="https://github.com/user-attachments/assets/23a28624-3da7-45b6-b586-1c45132bce3b" />
<img width="975" height="570" alt="image" src="https://github.com/user-attachments/assets/33c193b7-e301-48fa-b61e-3391f66300b6" />
<img width="975" height="518" alt="image" src="https://github.com/user-attachments/assets/535a4937-84a4-450e-a8b2-7de6dfccfef5" />
<img width="975" height="441" alt="image" src="https://github.com/user-attachments/assets/4bbcca5e-a8f6-4182-9285-0723fb3cf574" />
<img width="975" height="698" alt="image" src="https://github.com/user-attachments/assets/064782c9-9653-4082-98a4-8e05c8830c92" />
<img width="975" height="124" alt="image" src="https://github.com/user-attachments/assets/36456fe8-0c69-4e4c-abc9-a7dd4cace7a3" />
<img width="975" height="523" alt="image" src="https://github.com/user-attachments/assets/f1a7a7ef-27db-44de-998d-bc2e8e91c2ae" />
<img width="975" height="544" alt="image" src="https://github.com/user-attachments/assets/319c8fa6-e2a9-4c61-be7b-9dc29c2dff90" />
<img width="975" height="557" alt="image" src="https://github.com/user-attachments/assets/904d7868-fc94-4f5e-9c61-a2fb959f7bea" />

<img width="432" height="221" alt="image" src="https://github.com/user-attachments/assets/f5d58a55-d273-43e1-9995-7a677e540326" />

