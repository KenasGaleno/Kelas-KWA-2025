# SQL Injection Vulnerability Allowing Login Bypass

## 1. Objective
Melakukan eksploitasi **SQL Injection** pada form login untuk dapat mengakses aplikasi sebagai user **administrator** tanpa mengetahui password yang sah.



## 2. Tools
- **Burp Suite Community Edition** (untuk intercept dan modifikasi request).  
- **Web browser** (akses aplikasi target dari PortSwigger Academy).  

![WhatsApp Image 2025-09-10 at 17 42 18_816c1e4d](https://github.com/user-attachments/assets/5bbc4145-1e36-4762-845b-e7ea4b062634)


## 3. Steps

### Step 1 – Identifikasi Target
- Masuk ke halaman **Login** melalui menu *My account*.  
- Tersedia input **username** dan **password**.  
- Sesuai deskripsi lab, kita diminta login sebagai **administrator**.  

<img width="1460" height="737" alt="image" src="https://github.com/user-attachments/assets/e58488ab-661d-4174-a76f-8cfc356d8354" />


### Step 2 – Intercept Request
- Input sembarang data (misal `1234 : qwerty`).  
- Tangkap request dengan **Burp Proxy**.  
- Didapatkan body request:
  csrf=xxxx&username=1234&password=qwerty

<img width="1461" height="737" alt="image" src="https://github.com/user-attachments/assets/67fc79d4-50cf-4f8f-a340-84dd0a2acbf9" />


### Step 3 – Kirim ke Repeater
- Kirim request login ke **Repeater** untuk uji payload.  

![WhatsApp Image 2025-09-10 at 18 37 44_f7bc12b2](https://github.com/user-attachments/assets/f881248f-4a6d-4222-8497-490f1d143953)

![WhatsApp Image 2025-09-10 at 18 38 51_efff1879](https://github.com/user-attachments/assets/99443add-7c16-4b5f-98f9-3f25d56b532b)



### Step 4 – Testing SQL Injection Payload
- Untuk bypass login, gunakan payload:
username=administrator'--
password=abc

- `'` menutup string query.  
- `--` memberi komentar, sehingga validasi password diabaikan.
 
![WhatsApp Image 2025-09-10 at 18 40 48_666b853d](https://github.com/user-attachments/assets/ede93fbd-a3f4-4caf-97bb-0bcbd2d8fbbf)


### Step 5 – Verifikasi
- Setelah redirect, halaman **My Account** terbuka dengan username **administrator**.  
- Muncul notifikasi:

![WhatsApp Image 2025-09-10 at 18 40 10_503875f6](https://github.com/user-attachments/assets/3a4e0785-fcd1-4743-abbe-aa9c9e995abe)





