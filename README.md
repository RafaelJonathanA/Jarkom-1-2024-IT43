# Laporan Resmi Praktikum Modul 1 Jaringan Komputer

### Wireshark

### Kelompok IT43 -

| Name                              |     NRP    |
| ----------------------------------|------------|
| Rafael Jonathan Arnoldus          | 5027231006 | 
| Gandhi Ert Julio                  | 5027231081 |


---
---
---

## _Soal Advance Sanity Check_

#### Pertanyaan
- Username Pengirim
- Nama File Yang Dikirim
- String Rahasia

---

![image](https://github.com/user-attachments/assets/51dd38a0-2a03-4e34-b829-c3b152e7c419)
```
tcp 
```
Disini saya sudah pengfilteran `tcp`1 dan dari hasil capture ini saya mencari manual dimana isi paket/file yang berbeda dari yang lain.

![image](https://github.com/user-attachments/assets/697f5863-c757-4e20-a886-4e36a3cbfe6a)
![image](https://github.com/user-attachments/assets/d6db6291-555a-48ee-89a4-bbaedceef87d)
![image](https://github.com/user-attachments/assets/1a44bbd2-f210-466c-bac8-673acd5e20a6)

Lalu Terdapat beberapa hint dari hasil stream yang lainnya yang menunjukkan identitas username, Nama file yang dikirim dan petunjuk mendapatksan string password.

Lalu dengan mengikuti dan mengarah ke peraturan praktikunm yang tersedia didapatkan hasil string password yang ada

![image](https://github.com/user-attachments/assets/6483356f-c8e2-4933-9e9f-c2eeb116cb2d)
> Dengan encoding `base64` didapatkan hasilnya : `penword`

![image](https://github.com/user-attachments/assets/edd83288-c2fc-4478-bf98-ffe226dc9f8b)
> Pendapatan hasil Flag

nc 10.15.42.60 Port 44000


## _Soal FTP Login_

#### Pertanyaan
- Username sukses saat FTP Login
- Password sukses saat FTP Login

---

Dengan filtering `ftp` dan mencarinya secara manual
```
ftp
```
![image](https://github.com/user-attachments/assets/28c2480d-c184-4e35-b452-25bc9534269b)
> Didapatkan hasil saat tcp stream salah satu paket

![image](https://github.com/user-attachments/assets/804f54c5-488a-4c33-9c18-6355f2603caf)

Terlihat dari sini dimana username `sn34ky` dan password `sup3rsn1ff3r` lolos autentikasi user.

Lalu dengan mengakses Port 49000 terdapat pertanyaan tadi dalam meraih flag
![WhatsApp Image 2024-09-18 at 22 39 37_c9353e91](https://github.com/user-attachments/assets/4a501de6-6af2-4e98-bcb2-bc72b6e4d041)


## _Soal Surprise_

#### Pertanyaan

- Service dipakai di FTP server
- Nama file yang dikirim attacker
- Pesan rahasia ditinggalkan attacker

---

Dengan filtering paket dengan query `ftp.response.code == 220` yang merupakan respon dari server FTP saat koneksi pertama kali.
```
ftp.response.code == 220
```
![image](https://github.com/user-attachments/assets/d5dd91f7-feea-489a-afdc-328dc3798cf8)
> Dari tampilan capture sudah memberikan banner yang menampilkan service ver 

Mencari paket yang diupload menggunakan query `ftp.request.command == "STOR"`
```
ftp.request.command == "STOR"
```
![image](https://github.com/user-attachments/assets/d33fad29-5ca2-425a-a35f-6d911c372564)
> g0tcha.cpp

Lalu dengan Export code FTP data dan mengcompile file tersebut mendapatkan pesan rahasia

![WhatsApp Image 2024-09-18 at 21 50 58_bf8504b9](https://github.com/user-attachments/assets/b1232445-88d4-4b32-bedd-94aa15a4249d)
> Pertanyaan dan peraihan flag


## _Soal Illegal Breakthrough_

#### Pertanyaan

- IP Adress korban
- Port yang dipakai sebagai webserver
- Endpoint pada login
- Tools yang digunakan attacker
- Kredensial untuk login attacker

---

![image](https://github.com/user-attachments/assets/4e4a8053-5964-4ccf-83df-9c90bc584e40)

Pada capture tersebut terdapat komunikasi TCP 172.21.80.1 melakukan POST ke 172.21.88.207.

![image](https://github.com/user-attachments/assets/965086b8-84ff-458b-b524-7b699b6ffe43)
> Terlihat bahwa Source dan Destination, 1917 dipakai komunikasi HTTP ini. 
Dan dari capture tersebut sudah memberikan POST request ke ww1.php dengan data user dan pass. Menunjukkan jika itu adalah endpoint login.

![image](https://github.com/user-attachments/assets/9c9cef7c-51eb-46c6-9964-9ed9c96789de)

Dan pada bari User-Agent di heaeder http ini ada jejak dari toolsnya, `ffuf-v2.1.0-dev`

![image](https://github.com/user-attachments/assets/911d7fe1-3d6b-4c61-b5a0-7a9d80bd85b5)
> Mencari kredensial login attacker dengan filtering dan mendapatkan hasil

![WhatsApp Image 2024-09-18 at 21 50 00_3978c240](https://github.com/user-attachments/assets/149e947b-d9e7-419d-ad28-c3b7654b8db7)
> Pertanyaan dan peraihan flag

## _Soal Rizzset_

#### Pertanyaan

- Nama Domain dari dns query di log
- IP Domain
- Jarm fingerprint dihasilkan dari domain itu

---

![image](https://github.com/user-attachments/assets/7f04d8cd-14e6-435e-9e08-b2ac990055b4)

Terlihat dari hasil capture diatas ada query dns ke `www.its.ac.id`. dan IP nya yaitu `103.94.189.5`

Lalu menyiapkan JARM Fingerprint dan mencoba menjalankan JARM ke domain yang ingin di fingerprint
![WhatsApp Image 2024-09-18 at 21 48 58_01b60c29](https://github.com/user-attachments/assets/d2084b76-a37b-4848-a21c-fa463bc9dcbd)
> Hasil JARM Fingerprint

Lalu eksekusi ke PORT
![WhatsApp Image 2024-09-18 at 21 49 21_f8e3621a](https://github.com/user-attachments/assets/bc5ccdc7-163e-4d45-b93e-ee50f49b4a24)
> Pertanyaan dan peraihan flag

## _Soal FTP Login_

#### Pertanyaan

- Apa username yang berhasil digunakan untuk FTP login?
- Apa password yang berhasil digunakan untuk FTP login?


---

Pertama saya mendownload file yang ada
Kedua saya langsung memfilter dengan statistic lalu menu conversation lalu saya langsung mencari di setiap file yang ada dan saya menemukan usernamenya dan password yang digunakan 

Flag : JarkomIT{n0t_s0_s3cur3_ftp_sdFFEPlcdJNaE3Tn2fs1tpdihL0Y5goLWYNHcMsWAx4HKvKyV9j9G1N}

![FTP Login](https://github.com/user-attachments/assets/5c80992d-f74f-4501-858f-4e62b237bf28)

## _Soal Pegawai Negeri Sebelah_

#### Pertanyaan

- Siapa yang memiliki password nNnM%coQuF?
- Apa jabatan dari Taufan Kuswandari?
- Siapa yang paling awal di list?
- Apa password paling akhir dari list?


---

Pertama saya mendownload filenya lalu saya membuka dan menggunakan statistic dan conversation untuk melihat filenya lalu saya akan mencari password tersebut dengan searchnya lalu nama Taufan Kuswandari lalu melihat nama paling awal di list dan password paling akhir di list sehingga mendapatkan flagnya 

Flag : JarkomIT{Tum8eN_p45SnYa_Ku4t_B1aS4Nya_Hiow4mM5G172RSwBA8w8YJhWLL30AqhvwbyvDZrMNYRSAVwddw9vM4h}

[Pegawai Sebelah](https://github.com/user-attachments/assets/8bb7cb94-de77-4da2-a7ff-508f7b28285c)

## _Soal Corporate Breach _

#### Pertanyaan

- Siapa nama attacker?
- Apa email yang digunakan untuk login?
- Apa password yang digunakan untuk login?

---

Pertama saya mendownload file yang ada
Kedua saya langsung memfilter dengan statistic lalu menu conversation lalu saya cari mulai dari depan sampai ke paling akhir di file awal terdapat perkenalan dirinya sehingga saya mendapatkan nama attacker secara sekilas dan menemukan ada satu file yang berbeda pola formatnya dan langsung ketemu email serta password yang digunakan 

Flag : JarkomIT{supp0rt_k0k_l3m4h_bg_cv09tgcni7sDpEEaO4oyDxmfAG6XNddtZ7zBRYNW4NxDWSsDm3YwG6}

![breach](https://github.com/user-attachments/assets/25294662-9d4f-4b10-9814-01ead716dc76)

## _Soal Ez _

#### Pertanyaan

- Temukan jawaban dari log tersebut
- Port berapa yang digunakan service tersebut

---

Pertama Saya mendownload file yang ada lalu saya langsung menggunakan statistic dengan pilihan conversation lalu saya mengecek di file-file dan saya langsung menemukan jawabannya dan disaat yang sama portnya juga secara langsung terlihat 

Flag : JarkomIT{BiAr_aman_Pake_sSh_XhI4JDwoO9pxCSLUx9Rh3hrE43zSBorh9mFRyADDwCE0X0pq5yxXEZ}

![ez](https://github.com/user-attachments/assets/0dc5348a-e7fc-4523-b91f-ef0fa72d06a9)


## _Soal Malicious Code_

#### Pertanyaan

- Berapa total attempt attacker melakukan dir listing?
- Apa endpoint yang berhasil attacker dapatkan untuk login page?
- Pada attempt ke berapa attacker menemukan email dan password yang benar?
- Apa jawaban dari pertanyaan sang attacker?

---

Pertama saya buka file yang sama seperti saat mengerjakan soal corporate breach lalu saya menggunakan menu statistic dan conversation namun saya hanya menemukan pertanyaan yang berupa kode ascii yang perlu di ubah terlebih dahulu agar menjadi string yang dapat dibaca sehingga saya menggunakan filter http.request.method == "GET" untuk mendapatkan semua yang berupa request get yang kemudian dibuka melalui statistic untuk melihat jumlahnya, untuk endpoint saya menemukannya dengan filter http.request.method == "POST" untuk mendapatkan semua yang berupa request post yang kemudian saya dapatkan endpointnya, untuk yang terakhir setelah saya ubah saya dapatkan sebuah pertanyaan warna kesukaan pembuat soal dengan hint sweater, sehingga saya menjawab warna merah 

Flag : Benar! Ini flag-mu: JarkomIT{s3cr3t_m3ss4ge_fr0m_4uth0r_ZytXVTnBwhoyFIvyfW3Lk8naIC0T7J2hnXY5I9FDCm5yOQLiK73UL0R}

![malcious](https://github.com/user-attachments/assets/3f875dde-3cfe-4340-9e03-40ebf23e1782)

## _Soal Gajah terbang_

#### Pertanyaan

- Apa DBMS yang digunakan pada server tersebut?
- Di port berapa DBMS server tersebut berjalan?
- OS apa yang digunakan untuk server tersebut?
- Apa credentials username DBMS valid yang digunakan?
- Apa nama database yang digunakan?
- Ada berapa banyak users dalam database tersebut?
- Apa email yang digunakan oleh admin?
- Apa password yang digunakan oleh admin? 
---
Pertama saya membuka file gajah terbang lalu saya menggunakan statistic dan conversation untuk melihat isi dari file-filenya lalu saya mendapatkan namanya psql dan setelah itu saya mencari portnya dengan melihat dari tampilan dengan ada port berapa saja dan saya coba satu-satu sehigga mendapatkan port 6969 yang benar lalu di dalam file bila di perhatikan juga ada Debian sebagai OSnya lalu untuk nama username DBMS itu juga terlihat dari file yang ada langsung berapa pada bagian paling atas lalu untuk nama database juga sama langsung terlihat di bagian atas, jumlah user saya dapatkan dari menghitung manual pada isi file ada berapa banyak, dan unutuk password saya dapatkan dari file yang kemmudian harus di didecripsikan terlebihh dahulu

Flag : JarkomIT{Gy4tT_M5g_4U_GdGpusLONVeRns0bsCPDYOLvw5k1rq9fHseecDt9LCorWGnovNZgmBiD1}

![Gajah Terbang](https://github.com/user-attachments/assets/7ea8c5ea-c257-4704-9d21-42e108c212f2)

## Revisi
> Tidak ada
