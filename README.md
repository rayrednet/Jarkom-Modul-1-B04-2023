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

Langkah pertama, gunakan filter pada wireshark:

```http contains "Praktikum"```

Karena kita harus mencari web server maka protocol yang digunakan adalah `HTTP`, dan gunakan keyword pada filter `Praktikum` sebab kita harus mencari web server pada portal praktikum jaringan komputer. Filter tersebut akan mengeluarkan hasil sebagai berikut:

<img width="946" alt="image" src="https://github.com/rayrednet/Jarkom-Modul-1-B04-2023/assets/89933907/287c83ce-5cdd-40a9-9709-ea73eab6bb5e">

Langkah kedua, pilih packet yang pertama (memiliki tulisan `OK (text/html)`), klik kanan pilih `Follow -> HTTP Stream`. Akan terbuka window sebagai berikut:

<img width="958" alt="image" src="https://github.com/rayrednet/Jarkom-Modul-1-B04-2023/assets/89933907/32780dbe-70a0-4b51-a8ef-bc6dde1cc341">

Jadi, web server yang digunakan pada portal praktikum Jaringan Komputer adalah `gunicorn`

Flag yang kami peroleh untuk soal ini adalah sebagai berikut:

<img width="780" alt="image" src="https://github.com/rayrednet/Jarkom-Modul-1-B04-2023/assets/89933907/67ff7314-cf82-438f-ab9c-b9772751df90">

#### Kendala yang dialami
Belum ditemukan kendala saat mengerjakan soal nomor 2

### ⭐ Nomor 3
### Soal
Dapin sedang belajar analisis jaringan. Bantulah Dapin untuk mengerjakan soal berikut: <br />
a. Berapa banyak paket yang tercapture dengan IP source maupun destination address adalah 239.255.255.250 dengan port 3702? <br />
b. Protokol layer transport apa yang digunakan? <br />

### Jawaban:
#### Langkah Pengerjaan beserta Screenshot
Inilah tahapan yang telah kami lakukan untuk berhasil menyelesaikan soal ini: </br >

**3a. Banyak packet dengan IP source maupun destination address adalah 239.255.255.250 dengan port 3702**
Untuk melihat banyak packet sesuai dengan kriteria tersebut, gunakan filter pencarian berikut:

```
(ip.src == 239.255.255.250 && udp.port == 3702) || (ip.dst == 239.255.255.250 && udp.port == 3702)
```
- ip.src == 239.255.255.250 && udp.port == 3702: Ini berarti filter akan menangkap paket-paket yang memiliki alamat IP sumber (source) 239.255.255.250 dan port UDP 3702.

- ip.dst == 239.255.255.250 && udp.port == 3702: Ini berarti filter akan menangkap paket-paket yang memiliki alamat IP tujuan (destination) 239.255.255.250 dan port UDP 3702.

Penggunaan UDP dalam filter ini  disebabkan oleh jenis komunikasi atau lalu lintas yang dituju. Banyak aplikasi yang menggunakan UDP untuk komunikasi multicast atau broadcast, dan filter ini sepertinya dirancang untuk menangkap paket-paket yang terkait dengan komunikasi multicast yang memiliki alamat IP tertentu (239.255.255.250) dan port tertentu (3702).

<img width="960" alt="image" src="https://github.com/rayrednet/Jarkom-Modul-1-B04-2023/assets/89933907/adc045cd-908d-42ee-9789-aa94c1b794f1">

Pada bagian bawah, dapat dilihat `Displayed:21`, maka terdapat 21 packet yang memenuhi kriteria tersebut

**1b. Protokol layer transport yang digunakan**

Apabila kita mencari dengan filter UDP, SCTP, dan FTP berturut-turut diperoleh sebagai berikut:

<img width="957" alt="image" src="https://github.com/rayrednet/Jarkom-Modul-1-B04-2023/assets/89933907/7aa0aa36-bbe2-46a8-af17-321237ecf7d1">

<img width="958" alt="image" src="https://github.com/rayrednet/Jarkom-Modul-1-B04-2023/assets/89933907/1c93087b-1c10-4ec8-a035-e8546a24625d">

<img width="958" alt="image" src="https://github.com/rayrednet/Jarkom-Modul-1-B04-2023/assets/89933907/3eff64a9-cfc7-43e8-9cf6-938df80b22bf">

Maka dari itu protokol layer transport yang digunakan adalah `UDP`. Protokol layer transport bervariasi, tidak hanya 3 protokol itu, namun yang memenuhi kriteria soal 1a yang memungkinkan adalah ketiga layer transport tersebut.

Flag yang kami peroleh untuk soal ini adalah sebagai berikut:

<img width="878" alt="image" src="https://github.com/rayrednet/Jarkom-Modul-1-B04-2023/assets/89933907/9cc91f00-b9a3-40d6-aa62-105cc13dd132">

#### Kendala yang dialami
Belum ditemukan kendala dalam pengerjaan soal nomor 3

### ⭐ Nomor 4
### Soal
Berapa nilai checksum yang didapat dari header pada paket nomor 130?

### Jawaban:
#### Langkah Pengerjaan beserta Screenshot
Untuk mencapai penyelesaian masalah ini, kami telah melakukan langkah-langkah berikut: </br>

Langkah pertama, gunakan filter wireshark

`frame.number == 130`

Filter Wireshark frame.number == 130 digunakan untuk menangkap paket dengan nomor urut (sequence number) frame tertentu dalam capture. Maka, ketika kita menggunakan filter ini kita akan melihat atau menangkap paket yang memiliki nomor urut frame tepat 130 dalam capture tersebut.

Ketika filter tersebut dijalankan diperoleh:

<img width="958" alt="image" src="https://github.com/rayrednet/Jarkom-Modul-1-B04-2023/assets/89933907/1218b884-d53f-4ca4-ac57-848e71766579">

Langkah kedua, double click pada packet yang diperoleh dan expan pada bagian User Datagram Protocol. Disitu kita akan melihat nilai checksum
<img width="955" alt="image" src="https://github.com/rayrednet/Jarkom-Modul-1-B04-2023/assets/89933907/4418ca66-b9c8-4639-a7cc-11e47288cd85">

Jadi dapat dilihat bahwa nilai checksumnya adalah `0x18e5`

Flag yang kami peroleh untuk soal ini adalah sebagai berikut:

<img width="493" alt="Screenshot at 2023-09-18 21_51_54-(1) WhatsApp" src="https://github.com/rayrednet/Jarkom-Modul-1-B04-2023/assets/89933907/7df8203e-cdfc-48c3-861c-92326808d10f">

#### Kendala yang dialami
Belum ditemukan kendala dalam pengerjaan soal nomor 4

### ⭐ Nomor 5
### Soal
Elshe menemukan suatu file packet capture yang menarik. Bantulah Elshe untuk menganalisis file packet capture tersebut. <br />
a. Berapa banyak packet yang berhasil di capture dari file pcap tersebut? <br />
b. Port berapakah pada server yang digunakan untuk service SMTP? <br />
c. Dari semua alamat IP yang tercapture, IP berapakah yang merupakan public IP? <br />

### Jawaban:
#### Langkah Pengerjaan beserta Screenshot
Berikut ini adalah langkah-langkah yang kami lakukan untuk menyelesaikan soal ini: <br />
Langkah pertama, kita harus menemukan `nc` pada soal ini terlebih dahulu. Untuk mencarinya, kita lihat pada file `pcap` yang disediakan. Protokol SMTP merupakan protokol yang digunakan untuk mengirim email. Apabila kita melakukan follow TCP Stream pada salah satu packet SMTP kita akan memperoleh pesan tersembunyi sebagai berikut:

<img width="959" alt="image" src="https://github.com/rayrednet/Jarkom-Modul-1-B04-2023/assets/89933907/40b11b36-798c-4f9c-b16f-0b1c726e39e0">

Pada soal ini juga terdapat file .zip yang diberi password untuk membukanya. Untuk mengetahui password dari file zip tersebut, kita harus melakukan decrypt sesuai yang tertera pada email tersebut. Kami menggunakan bantuan dari https://www.base64decode.org/ untuk melakukan dekripsi yang diperoleh sebagai berikut:

<img width="369" alt="image" src="https://github.com/rayrednet/Jarkom-Modul-1-B04-2023/assets/89933907/16befc01-cdb4-4389-b99d-91dc19fbfb15">

Maka, password dari file .zip tersebut adalah `5implePas5word`. Setelah itu, kita unzip file zip dan ditemukan file .txt yang berisi `nc` soal sebagai berikut:

<img width="246" alt="image" src="https://github.com/rayrednet/Jarkom-Modul-1-B04-2023/assets/89933907/c1d809ef-d5a8-422b-939f-4cbfd47dd775">

**5a. Banyak packet di file pcap**

Banyaknya packet yang tercapture dapat dilihat di bagian bawah kanan wireshark, yaitu `60` packet.

<img width="957" alt="image" src="https://github.com/rayrednet/Jarkom-Modul-1-B04-2023/assets/89933907/2e51c13f-4bdb-4eb8-8c06-552de36b9224">

**5b. Port yang digunakan pada server untuk service SMTP**

Flag yang kami peroleh untuk soal ini adalah sebagai berikut:

<img width="309" alt="image" src="https://github.com/rayrednet/Jarkom-Modul-1-B04-2023/assets/89933907/6b67a613-9ed1-4628-b26c-3aa10b801007">

#### Kendala yang dialami

### ⭐ Nomor 6
### Soal
Seorang anak bernama Udin Berteman dengan SlameT yang merupakan seorang penggemar film detektif. sebagai teman yang baik, Ia selalu mengajak slamet untuk bermain valoranT bersama. suatu malam, terjadi sebuah hal yang tak terdUga. ketika udin mereka membuka game tersebut, laptop udin menunjukkan sebuah field text dan Sebuah kode Invalid bertuliskan "server SOURCE ADDRESS 7812 is invalid". ketika ditelusuri di google, hasil pencarian hanya menampilkan a1 e5 u21. jiwa detektif slamet pun bergejolak. bantulah udin dan slamet untuk menemukan solusi kode error tersebut.

### Jawaban:
#### Langkah Pengerjaan beserta Screenshot
Langkah-langkah yang telah kami terapkan untuk menyelesaikan tugas ini adalah sebagai berikut: <br />
Flag yang kami peroleh untuk soal ini adalah sebagai berikut:

#### Kendala yang dialami

### ⭐ Nomor 7
### Soal
Berapa jumlah packet yang menuju IP 184.87.193.88?

### Jawaban:
#### Langkah Pengerjaan beserta Screenshot
Inilah tahapan yang telah kami lakukan untuk berhasil menyelesaikan soal ini: </br >
Flag yang kami peroleh untuk soal ini adalah sebagai berikut:

#### Kendala yang dialami

### ⭐ Nomor 8
### Soal
Berikan kueri filter sehingga wireshark hanya mengambil semua protokol paket yang menuju port 80! (Jika terdapat lebih dari 1 port, maka urutkan sesuai dengan abjad)

### Jawaban:
#### Langkah Pengerjaan beserta Screenshot
Langkah-langkah yang telah kami terapkan untuk menyelesaikan tugas ini adalah sebagai berikut: <br />
Flag yang kami peroleh untuk soal ini adalah sebagai berikut:

#### Kendala yang dialami

### ⭐ Nomor 9
### Soal
Berikan kueri filter sehingga wireshark hanya mengambil paket yang berasal dari alamat 10.51.40.1 tetapi tidak menuju ke alamat 10.39.55.34!

### Jawaban:
#### Langkah Pengerjaan beserta Screenshot
Langkah-langkah yang telah kami terapkan untuk menyelesaikan tugas ini adalah sebagai berikut: <br />
Flag yang kami peroleh untuk soal ini adalah sebagai berikut:

#### Kendala yang dialami

### ⭐ Nomor 10
### Soal
Sebutkan kredensial yang benar ketika user mencoba login menggunakan Telnet

### Jawaban:
#### Langkah Pengerjaan beserta Screenshot
Berikut ini adalah langkah-langkah yang kami lakukan untuk menyelesaikan soal ini: <br />
Flag yang kami peroleh untuk soal ini adalah sebagai berikut:

#### Kendala yang dialami
