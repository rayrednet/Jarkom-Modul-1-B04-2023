# Laporan Resmi Praktikum Jaringan Komputer Modul 1 - Crimping & Wireshark

## Daftar Isi
[Nomor 1 - Addressing](https://github.com/rayrednet/Jarkom-Modul-1-B04-2023#-nomor-1) <br/>
[Nomor 2 - Stream](https://github.com/rayrednet/Jarkom-Modul-1-B04-2023#-nomor-2) <br/>
[Nomor 3 - Analysis](https://github.com/rayrednet/Jarkom-Modul-1-B04-2023#-nomor-3) <br/>
[Nomor 4 - Addressing](https://github.com/rayrednet/Jarkom-Modul-1-B04-2023#-nomor-4) <br/>
[Nomor 5 - Analysis](https://github.com/rayrednet/Jarkom-Modul-1-B04-2023#-nomor-5) <br/>
[Nomor 6 - Addressing](https://github.com/rayrednet/Jarkom-Modul-1-B04-2023#-nomor-6) <br/>
[Nomor 7 - Filtering](https://github.com/rayrednet/Jarkom-Modul-1-B04-2023#-nomor-7) <br/>
[Nomor 8 - Filtering](https://github.com/rayrednet/Jarkom-Modul-1-B04-2023#-nomor-8) <br/>
[Nomor 9 - Filtering](https://github.com/rayrednet/Jarkom-Modul-1-B04-2023#-nomor-9) <br/>
[Nomor 10 - Stream](https://github.com/rayrednet/Jarkom-Modul-1-B04-2023#-nomor-10) <br/>


## Identitas Kelompok
| Nama                                 | NRP        |
| -------------------------------------|------------|
| Rayssa Ravelia                       | 5025211219 |
| Immanuel Pascanov Samosir            | 5025211257 |

### ⭐ Nomor 1
### Soal
User melakukan berbagai aktivitas dengan menggunakan protokol FTP. Salah satunya adalah mengunggah suatu file. <br/>
a. Berapakah sequence number (raw) pada packet yang menunjukkan aktivitas tersebut? <br/>
b. Berapakah acknowledge number (raw) pada packet yang menunjukkan aktivitas tersebut? <br/>
c. Berapakah sequence number (raw) pada packet yang menunjukkan response dari aktivitas tersebut? <br/>
d. Berapakah acknowledge number (raw) pada packet yang menunjukkan response dari aktivitas tersebut? <br/>


### Jawaban:
#### Langkah Pengerjaan beserta Screenshot
Berikut ini adalah langkah-langkah yang kami lakukan untuk menyelesaikan soal ini: <br />

**1a. Sequence number (raw) pada packet aktivitas mengunggah suatu file** <br />
Langkah pertama adalah melakukan filter di wireshark sebagai berikut: <br/ >
```ftp.request.command == STOR ``` <br />
Perintah filter terserbut akan melakukan penyaringan pada lalu lintas jaringan yang mengandung perintah FTP (File Transfer Protocol) yang memiliki perintah "STOR". 
- ftp.request.command: Bagian ini adalah bagian pertama dari filter. Ini mengacu pada protokol FTP dan mengidentifikasi paket-paket yang berisi perintah FTP yang dikirimkan dari klien FTP ke server FTP.
- ==: Ini adalah operator perbandingan yang digunakan untuk memeriksa apakah nilai di sebelah kiri sama dengan nilai di sebelah kanan.
- STOR: Ini adalah perintah FTP yang digunakan untuk mengunggah (upload) file ke server FTP
Dari filter tersebut, akan menghasilkan keluaran 1 paket sebagai berikut:

<img width="958" alt="image" src="https://github.com/rayrednet/Jarkom-Modul-1-B04-2023/assets/89933907/0a13ab79-650c-4ac8-b03a-1508c1e441af">

Langkah kedua, kita lihat detail paket dengan cara double klik pada paket tersebut, kemudian expand bagian Transimission Control Protocol

<img width="956" alt="image" src="https://github.com/rayrednet/Jarkom-Modul-1-B04-2023/assets/89933907/0d8762f9-0d43-415a-bf50-f145a6f0ee3b">

Dari informasi di atas, dapat dilihat bahwa sequence number (raw) pada packet yang dimaksud adalah `258040667`

**1b. Acknowledge number (raw) pada packet aktivitas mengunggah suatu file** <br />
Untuk melihat acknowledge number (raw) pada packet tersebut, kita dapat scroll ke bawah di bagian Transimission Control Protocol, sehingga diperoleh sebagai berikut:

<img width="961" alt="image" src="https://github.com/rayrednet/Jarkom-Modul-1-B04-2023/assets/89933907/e8439880-2f1d-45af-b9a6-d857620508e7">

Maka, dapat dilihat bahwa acknowledge number (raw) pada packet aktivitas mengunggah suatu file adalah `1044861039`

**1c. Sequence number (raw) pada packet yang menunjukkan response dari aktivitas tersebut** <br />
Untuk mencari response dari aktivitas yang dimaksud, gunakan filter wireshark berikut:

```
ftp contains "GrabThePhisher"
```

Filter Wireshark tersebut digunakan untuk menyaring semua paket dalam capture yang mengandung string "GrabThePhisher" dalam lalu lintas FTP. String "GrabThePhisher" merupakan bagian daru request yang dimaksud pada soal tersebut. Setelah filter dijalankan, akan keluar output sebagai berikut:

<img width="956" alt="image" src="https://github.com/rayrednet/Jarkom-Modul-1-B04-2023/assets/89933907/68e41480-9608-4222-9518-05e32aa5e545">

Selanjutnya, double click pada packet yang memiliki `Info Response` untuk melihat detail pada bagian Transimission Control Protocol

<img width="960" alt="image" src="https://github.com/rayrednet/Jarkom-Modul-1-B04-2023/assets/89933907/9fe77c9c-6243-43e2-9211-e06abb8ea232">

Dapat dilihat bahwa sequence number (raw) pada packet yang menunjukkan response dari aktivitas tersebut adalah `1044861039`

**1d. Acknowledge number (raw) pada packet yang menunjukkan response dari aktivitas tersebut** <br />

Acknowledge number (raw) pada response aktivitas berada pada bagian Transimission Control Protocol. Maka, kita hanya perlu scroll ke bawah pada bagian Transimission Control Protocol sebagai berikut:

<img width="954" alt="image" src="https://github.com/rayrednet/Jarkom-Modul-1-B04-2023/assets/89933907/0c6e059b-c79b-4a53-a844-bde34901c307">

Dapat dilihat bahwa acknowledge number (raw) pada packet yang menunjukkan response dari aktivitas tersebut adalah `258040696`

Flag yang kami peroleh untuk soal ini adalah sebagai berikut:

<img width="747" alt="Screenshot at 2023-09-18 21_48_30-Filter Wireshark FTP STOR" src="https://github.com/rayrednet/Jarkom-Modul-1-B04-2023/assets/89933907/a661f78e-1177-4c78-9859-29a832e9a39d">

#### Kendala yang dialami

Belum ditemukan kendala saat mengerjakan soal nomor 1

### ⭐ Nomor 2
### Soal
Sebutkan web server yang digunakan pada portal praktikum Jaringan Komputer!

### Jawaban:
#### Langkah Pengerjaan beserta Screenshot
Langkah-langkah yang telah kami terapkan untuk menyelesaikan tugas ini adalah sebagai berikut: <br />

#### Kendala yang dialami


### ⭐ Nomor 3
### Soal
Dapin sedang belajar analisis jaringan. Bantulah Dapin untuk mengerjakan soal berikut: <br />
a. Berapa banyak paket yang tercapture dengan IP source maupun destination address adalah 239.255.255.250 dengan port 3702? <br />
b. Protokol layer transport apa yang digunakan? <br />

### Jawaban:
#### Langkah Pengerjaan beserta Screenshot
Inilah tahapan yang telah kami lakukan untuk berhasil menyelesaikan soal ini: </br >

#### Kendala yang dialami

### ⭐ Nomor 4
### Soal
Berapa nilai checksum yang didapat dari header pada paket nomor 130?

### Jawaban:
#### Langkah Pengerjaan beserta Screenshot
Untuk mencapai penyelesaian masalah ini, kami telah melakukan langkah-langkah berikut: </br>

#### Kendala yang dialami

### ⭐ Nomor 5
### Soal
Elshe menemukan suatu file packet capture yang menarik. Bantulah Elshe untuk menganalisis file packet capture tersebut. <br />
a. Berapa banyak packet yang berhasil di capture dari file pcap tersebut? <br />
b. Port berapakah pada server yang digunakan untuk service SMTP? <br />
c. Dari semua alamat IP yang tercapture, IP berapakah yang merupakan public IP? <br />

### Jawaban:
#### Langkah Pengerjaan beserta Screenshot
Berikut ini adalah langkah-langkah yang kami lakukan untuk menyelesaikan soal ini: <br />

#### Kendala yang dialami

### ⭐ Nomor 6
### Soal
Seorang anak bernama Udin Berteman dengan SlameT yang merupakan seorang penggemar film detektif. sebagai teman yang baik, Ia selalu mengajak slamet untuk bermain valoranT bersama. suatu malam, terjadi sebuah hal yang tak terdUga. ketika udin mereka membuka game tersebut, laptop udin menunjukkan sebuah field text dan Sebuah kode Invalid bertuliskan "server SOURCE ADDRESS 7812 is invalid". ketika ditelusuri di google, hasil pencarian hanya menampilkan a1 e5 u21. jiwa detektif slamet pun bergejolak. bantulah udin dan slamet untuk menemukan solusi kode error tersebut.

### Jawaban:
#### Langkah Pengerjaan beserta Screenshot
Langkah-langkah yang telah kami terapkan untuk menyelesaikan tugas ini adalah sebagai berikut: <br />

#### Kendala yang dialami

### ⭐ Nomor 7
### Soal
Berapa jumlah packet yang menuju IP 184.87.193.88?

### Jawaban:
#### Langkah Pengerjaan beserta Screenshot
Inilah tahapan yang telah kami lakukan untuk berhasil menyelesaikan soal ini: </br >

#### Kendala yang dialami

### ⭐ Nomor 8
### Soal
Berikan kueri filter sehingga wireshark hanya mengambil semua protokol paket yang menuju port 80! (Jika terdapat lebih dari 1 port, maka urutkan sesuai dengan abjad)

### Jawaban:
#### Langkah Pengerjaan beserta Screenshot
Langkah-langkah yang telah kami terapkan untuk menyelesaikan tugas ini adalah sebagai berikut: <br />

#### Kendala yang dialami

### ⭐ Nomor 9
### Soal
Berikan kueri filter sehingga wireshark hanya mengambil paket yang berasal dari alamat 10.51.40.1 tetapi tidak menuju ke alamat 10.39.55.34!

### Jawaban:
#### Langkah Pengerjaan beserta Screenshot
Langkah-langkah yang telah kami terapkan untuk menyelesaikan tugas ini adalah sebagai berikut: <br />

#### Kendala yang dialami

### ⭐ Nomor 10
### Soal
Sebutkan kredensial yang benar ketika user mencoba login menggunakan Telnet

### Jawaban:
#### Langkah Pengerjaan beserta Screenshot
Berikut ini adalah langkah-langkah yang kami lakukan untuk menyelesaikan soal ini: <br />

#### Kendala yang dialami
