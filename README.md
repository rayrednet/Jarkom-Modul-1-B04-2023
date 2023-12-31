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

**1a. Sequence number (raw) pada packet aktivitas mengunggah suatu file** 

Langkah pertama adalah melakukan filter di wireshark sebagai berikut:

```ftp.request.command == STOR ``` <br />

Perintah filter terserbut akan melakukan penyaringan pada lalu lintas jaringan yang mengandung perintah FTP (File Transfer Protocol) yang memiliki perintah "STOR". 
- ftp.request.command: Bagian ini adalah bagian pertama dari filter. Ini mengacu pada protokol FTP dan mengidentifikasi paket-paket yang berisi perintah FTP yang dikirimkan dari klien FTP ke server FTP.
- ==: Ini adalah operator perbandingan yang digunakan untuk memeriksa apakah nilai di sebelah kiri sama dengan nilai di sebelah kanan.
- STOR: Ini adalah perintah FTP yang digunakan untuk mengunggah (upload) file ke server FTP
Dari filter tersebut, akan menghasilkan keluaran 1 paket sebagai berikut:

<img width="958" alt="Screenshot at 2023-09-22 06_19_46-Settings" src="https://github.com/rayrednet/Jarkom-Modul-1-B04-2023/assets/89933907/f9577de8-3c2a-46fd-8f4c-8075f6bcd787">

Langkah kedua, kita lihat detail paket dengan cara double klik pada paket tersebut, kemudian expand bagian `Transmission Control Protocol`

<img width="956" alt="Screenshot at 2023-09-22 06_22_04-Settings" src="https://github.com/rayrednet/Jarkom-Modul-1-B04-2023/assets/89933907/3abcf5ac-bee6-4e3e-8235-59dbb08a5a63">

Dari informasi di atas, dapat dilihat bahwa sequence number (raw) pada packet yang dimaksud adalah `258040667`

**1b. Acknowledge number (raw) pada packet aktivitas mengunggah suatu file** <br />
Untuk melihat acknowledge number (raw) pada packet tersebut, kita dapat scroll ke bawah di bagian `Transimission Control Protocol`, sehingga diperoleh sebagai berikut:

<img width="961" alt="Screenshot at 2023-09-22 06_27_10-Jarkom-Modul-1-B04-2023 - Google Drive" src="https://github.com/rayrednet/Jarkom-Modul-1-B04-2023/assets/89933907/2b9968e1-066e-46f8-89e6-c9f41cb6fc96">

Maka, dapat dilihat bahwa acknowledge number (raw) pada packet aktivitas mengunggah suatu file adalah `1044861039`

**1c. Sequence number (raw) pada packet yang menunjukkan response dari aktivitas tersebut** <br />
Untuk mencari response dari aktivitas yang dimaksud, gunakan filter wireshark berikut:

```
ftp contains "GrabThePhisher"
```

Filter Wireshark tersebut digunakan untuk menyaring semua paket dalam capture yang mengandung string "GrabThePhisher" dalam lalu lintas FTP. String "GrabThePhisher" merupakan bagian daru request yang dimaksud pada soal tersebut. Setelah filter dijalankan, akan keluar output sebagai berikut:

<img width="956" alt="Screenshot at 2023-09-22 06_33_05-Settings" src="https://github.com/rayrednet/Jarkom-Modul-1-B04-2023/assets/89933907/d94b7c75-adf6-4667-bc80-aa05825d091a">

Selanjutnya, double click pada packet yang memiliki `Info Response` untuk melihat detail pada bagian `Transimission Control Protocol`

<img width="960" alt="Screenshot at 2023-09-22 06_36_27-Settings" src="https://github.com/rayrednet/Jarkom-Modul-1-B04-2023/assets/89933907/bd2eac0e-a751-4484-a774-827ff04b4d8d">

Dapat dilihat bahwa sequence number (raw) pada packet yang menunjukkan response dari aktivitas tersebut adalah `1044861039`

**1d. Acknowledge number (raw) pada packet yang menunjukkan response dari aktivitas tersebut** <br />

Acknowledge number (raw) pada response aktivitas berada pada bagian Transimission Control Protocol. Maka, kita hanya perlu scroll ke bawah pada bagian Transimission Control Protocol sebagai berikut:

<img width="954" alt="Screenshot at 2023-09-22 06_39_00-Settings" src="https://github.com/rayrednet/Jarkom-Modul-1-B04-2023/assets/89933907/9a81de95-e01d-4309-afa5-5b3521b33d29">

Dapat dilihat bahwa acknowledge number (raw) pada packet yang menunjukkan response dari aktivitas tersebut adalah `258040696`

Flag yang kami peroleh untuk soal ini adalah sebagai berikut:

<img width="747" alt="Screenshot at 2023-09-18 21_48_30-Filter Wireshark FTP STOR" src="https://github.com/rayrednet/Jarkom-Modul-1-B04-2023/assets/89933907/83ef0c7c-22a6-4539-b187-0f9ab98e6838">

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

<img width="946" alt="Screenshot at 2023-09-22 06_48_31-Settings" src="https://github.com/rayrednet/Jarkom-Modul-1-B04-2023/assets/89933907/cde87086-defc-4a2b-9e89-cf0fa658818f">

Langkah kedua, pilih packet yang pertama (memiliki tulisan `OK (text/html)`), klik kanan pilih `Follow -> HTTP Stream`. Akan terbuka window sebagai berikut:

<img width="958" alt="Screenshot at 2023-09-22 06_52_17-" src="https://github.com/rayrednet/Jarkom-Modul-1-B04-2023/assets/89933907/dff94ca1-effe-4373-bd70-96855ed682c0">

Jadi, web server yang digunakan pada portal praktikum Jaringan Komputer adalah `gunicorn`

Flag yang kami peroleh untuk soal ini adalah sebagai berikut:

<img width="780" alt="Screenshot at 2023-09-22 06_55_13-Screenshot at 2023-09-18 21_51_20-(1) WhatsApp png ‎- Photos" src="https://github.com/rayrednet/Jarkom-Modul-1-B04-2023/assets/89933907/0d72d44a-cf50-4709-bdc5-d1fbbfb2fcf6">

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

<img width="960" alt="Screenshot at 2023-09-22 07_00_29-Photos" src="https://github.com/rayrednet/Jarkom-Modul-1-B04-2023/assets/89933907/b34c1c63-1555-4bb5-9681-664e10dd23f6">

Pada bagian bawah, dapat dilihat `Displayed:21`, maka terdapat 21 packet yang memenuhi kriteria tersebut

**1b. Protokol layer transport yang digunakan**

Apabila kita mencari dengan filter UDP, SCTP, dan FTP berturut-turut diperoleh sebagai berikut:

<img width="957" alt="Screenshot at 2023-09-22 07_09_41-Settings" src="https://github.com/rayrednet/Jarkom-Modul-1-B04-2023/assets/89933907/9e3f2e27-c2a5-4f84-be71-e781081dcb0e">

<img width="958" alt="Screenshot at 2023-09-22 07_10_04-Settings" src="https://github.com/rayrednet/Jarkom-Modul-1-B04-2023/assets/89933907/089e275f-52fc-41f6-939f-3a8178dbb6cc">

<img width="958" alt="Screenshot at 2023-09-22 07_10_17-Settings" src="https://github.com/rayrednet/Jarkom-Modul-1-B04-2023/assets/89933907/0221bf24-d8ca-4b84-8d1e-263a3e173e4f">

Maka dari itu protokol layer transport yang digunakan adalah `UDP`. Protokol layer transport bervariasi, tidak hanya 3 protokol itu, namun yang memenuhi kriteria soal 1a yang memungkinkan adalah ketiga layer transport tersebut.

Flag yang kami peroleh untuk soal ini adalah sebagai berikut:

<img width="878" alt="Screenshot at 2023-09-22 07_05_10-Screenshot at 2023-09-18 19_26_36-Greenshot png ‎- Photos" src="https://github.com/rayrednet/Jarkom-Modul-1-B04-2023/assets/89933907/13a93701-0c22-4681-937e-4801455e0ff3">

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

<img width="958" alt="Screenshot at 2023-09-22 07_20_05-Settings" src="https://github.com/rayrednet/Jarkom-Modul-1-B04-2023/assets/89933907/ec81f342-b48e-42d6-ba2e-c308c6758672">

Langkah kedua, double click pada packet yang diperoleh dan expand pada bagian `User Datagram Protocol`. Disitu kita akan melihat nilai checksum

<img width="955" alt="Screenshot at 2023-09-22 07_21_02-Settings" src="https://github.com/rayrednet/Jarkom-Modul-1-B04-2023/assets/89933907/38f32782-ffe0-4157-967d-0162a2dd1bd6">

Jadi dapat dilihat bahwa nilai checksumnya adalah `0x18e5`

Flag yang kami peroleh untuk soal ini adalah sebagai berikut:

<img width="493" alt="Screenshot at 2023-09-18 21_51_54-(1) WhatsApp" src="https://github.com/rayrednet/Jarkom-Modul-1-B04-2023/assets/89933907/79d6bd66-8c60-4de0-abea-a5aac35bfda8">

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

<img width="955" alt="Screenshot at 2023-09-22 07_31_42-Settings" src="https://github.com/rayrednet/Jarkom-Modul-1-B04-2023/assets/89933907/87a8ab8e-015d-4d43-8597-56132b02253e">

Pada soal ini juga terdapat file .zip yang diberi password untuk membukanya. Untuk mengetahui password dari file zip tersebut, kita harus melakukan decrypt sesuai yang tertera pada email tersebut. Kami menggunakan bantuan dari https://www.base64decode.org/ untuk melakukan dekripsi yang diperoleh sebagai berikut:

<img width="369" alt="Screenshot at 2023-09-22 07_40_12-Base64 Decode and Encode - Online" src="https://github.com/rayrednet/Jarkom-Modul-1-B04-2023/assets/89933907/9947c22e-7f32-4756-8093-e8313b8a6c3d">


Maka, password dari file .zip tersebut adalah `5implePas5word`. Setelah itu, kita unzip file zip dan ditemukan file .txt yang berisi `nc` soal sebagai berikut:

<img width="246" alt="image" src="https://github.com/rayrednet/Jarkom-Modul-1-B04-2023/assets/89933907/2381a674-97eb-42fa-9822-9f518124f15e">

**5a. Banyak packet di file pcap**

Banyaknya packet yang tercapture dapat dilihat di bagian bawah kanan wireshark, yaitu `60` packet.

<img width="957" alt="Screenshot at 2023-09-22 07_45_53-Settings" src="https://github.com/rayrednet/Jarkom-Modul-1-B04-2023/assets/89933907/10173857-abec-4c21-b6c1-fe51f30922ae">

**5b. Port yang digunakan pada server untuk service SMTP**
Untuk melihat banyaknya port yang digunakan, klik salah satu detail service SMTP dan expand bagian `Transmission Control Protocol`

<img width="952" alt="Screenshot at 2023-09-22 08_10_22-soal5 pcap" src="https://github.com/rayrednet/Jarkom-Modul-1-B04-2023/assets/89933907/9a43e1e9-43b1-4028-9f2a-9e5212cdecd1">

Pada section `Destination Port` dapat dilihat bahwa banyaknya port yang digunakan adalah sebanyak `25`

**5c. IP Public yang ter-capture**
Untuk menentukan IP Public kita mengetahui bahwa untuk IP Private berkisar dari range `10.0.0.0` hingga `10.255.255.255`, `172.16.0.0` hingga `171.31.255.255`, dan `192.168.0.0` hingga `192.168.255.255`. Di luar range tersebut merupakan IP Public. Berdasarkan analisis IP pada file tersebut, yang merupakan IP Public yang tercapture adalah `74.53.140.153`

<img width="961" alt="Screenshot at 2023-09-22 08_11_57-Jarkom-Modul-1-B04-2023 - Google Drive" src="https://github.com/rayrednet/Jarkom-Modul-1-B04-2023/assets/89933907/69e7f7c5-eaaa-4a18-91be-708e35d5428c">

Flag yang kami peroleh untuk soal ini adalah sebagai berikut:

<img width="576" alt="Screenshot at 2023-09-18 21_52_24-(1) WhatsApp" src="https://github.com/rayrednet/Jarkom-Modul-1-B04-2023/assets/89933907/52f36098-03bb-4306-98d2-4ebddb66d197">

#### Kendala yang dialami
Kami sempat mengalami kendala untuk mendapatkan kode nc soal, namun masalah tersebut dapat teratasi saat praktikum berlangsung

### ⭐ Nomor 6
### Soal
Seorang anak bernama Udin Berteman dengan SlameT yang merupakan seorang penggemar film detektif. sebagai teman yang baik, Ia selalu mengajak slamet untuk bermain valoranT bersama. suatu malam, terjadi sebuah hal yang tak terdUga. ketika udin mereka membuka game tersebut, laptop udin menunjukkan sebuah field text dan Sebuah kode Invalid bertuliskan "server SOURCE ADDRESS 7812 is invalid". ketika ditelusuri di google, hasil pencarian hanya menampilkan a1 e5 u21. jiwa detektif slamet pun bergejolak. bantulah udin dan slamet untuk menemukan solusi kode error tersebut.

### Jawaban:
#### Langkah Pengerjaan beserta Screenshot
Langkah-langkah yang telah kami terapkan untuk menyelesaikan tugas ini adalah sebagai berikut: <br />
Langkah pertama, menggunakan filter untuk mencari `frame.number == 7812` sebab pada soal diketahui `server SOURCE ADDRESS 7812 is invalid` yang merupakan clue dari nomor paket. Diperoleh hasil filter sebagai berikut:

<img width="958" alt="Screenshot at 2023-09-22 08_20_56-Settings" src="https://github.com/rayrednet/Jarkom-Modul-1-B04-2023/assets/89933907/79084579-c2cf-43f7-8bb7-5218dbd80756">

Langkah kedua, apabila kita menganalisis pada soal tersebut, terdapat beberapa kata yang kapital tidak sesuai dengan aturan tata bahasa. Jika kita gabungkan huruf kapital tersebut akan membentuk kata `SUBSTITUSI`

<img width="716" alt="Screenshot at 2023-09-22 08_25_04-Seorang anak bernama Udin Berteman dengan SlameT yang merupakan seorang penggema" src="https://github.com/rayrednet/Jarkom-Modul-1-B04-2023/assets/89933907/b3fee07f-0c89-466d-b9b0-1a9549f8a8ad">


Langkah ketiga, pada soal juga terdapat clue `a1 e5 u21`. Jika kita perhatikan clue tersebut menunjuk kepada alfabet dan urutannya, sebagai berikut:

![alphabet-numbers](https://github.com/rayrednet/Jarkom-Modul-1-B04-2023/assets/89933907/685a8350-6181-47a7-9694-8563bfce00fb)

Langkah keempat, IP pada packet 7812 adalah `104.18.14.101`, jika kita melakukan substitusi angka tersebut menjadi huruf maka:

```
104.18.14.101
10 4 18 14 10 1

10 = J
4 = D
18 = R
14 = N
10 = J
1 = A

JDRNJA
```

Jadi, solusi dari soal ini adalah `JDRNJA`

Flag yang kami peroleh untuk soal ini adalah sebagai berikut:

<img width="944" alt="Screenshot at 2023-09-22 08_19_14-soal6-9 pcapng" src="https://github.com/rayrednet/Jarkom-Modul-1-B04-2023/assets/89933907/1993167b-b09c-41ca-bbb2-b4564bcc0811">


#### Kendala yang dialami
Pada saat praktikum, kami tidak membuka hint soal sama sekali sehingga tidak mampu menyelesaikannya saat masa praktikum, namun kami dapat menyelesaikannya saat masa revisi.

### ⭐ Nomor 7
### Soal
Berapa jumlah packet yang menuju IP 184.87.193.88?

### Jawaban:
#### Langkah Pengerjaan beserta Screenshot
Inilah tahapan yang telah kami lakukan untuk berhasil menyelesaikan soal ini: </br >

Langkah pertama untuk mencari jumlah packet yang menuju `IP 184.87.193.88` pada `soal6-9.pcapng`, dengan menggunakan filter expression `ip.dst == 184.87.193.88`, yang mana artinya paket mana saja yang menuju alamat ip 184.87.193.88

<img width="1265" alt="soal7part1" src="https://github.com/rayrednet/Jarkom-Modul-1-B04-2023/assets/89269231/cdf208b4-1051-4f23-8109-9b006b43c9ca">

Lalu yang terakhir dan sesuai pada screenshot dibawah, jumlah packet yang terdisplay menuju alamat IP tersebut adalah 6.

<img width="958" alt="image" src="https://github.com/rayrednet/Jarkom-Modul-1-B04-2023/assets/89933907/ed429885-2831-4ebb-8eff-9dcabc34699a">

<img width="276" alt="soal7part2" src="https://github.com/rayrednet/Jarkom-Modul-1-B04-2023/assets/89269231/816feb51-c45c-4ffc-8fd2-43f6f5a8245c">

Flag yang kami peroleh untuk soal ini adalah sebagai berikut:

![soal7flag](https://github.com/rayrednet/Jarkom-Modul-1-B04-2023/assets/89269231/351d809f-b2e5-4115-8ce0-207c5e009606)

#### Kendala yang dialami

Belum ditemukan kendala dalam pengerjaan soal nomor 7

### ⭐ Nomor 8
### Soal
Berikan kueri filter sehingga wireshark hanya mengambil semua protokol paket yang menuju port 80! (Jika terdapat lebih dari 1 port, maka urutkan sesuai dengan abjad)

### Jawaban:
#### Langkah Pengerjaan beserta Screenshot
Langkah-langkah yang telah kami terapkan untuk menyelesaikan tugas ini adalah sebagai berikut: <br />

Langkah pertama untuk mengambil semua protokol yang menuju port 80, kita dapat menggunakan filter expression ini `(tcp.dstport == 80 || udp.dstport == 80)`, digunakan untuk mencari paket-paket yang memiliki port tujuan (dstport) 80 baik menggunakan protokol TCP atau UDP.

<img width="958" alt="image" src="https://github.com/rayrednet/Jarkom-Modul-1-B04-2023/assets/89933907/6b957a43-7abb-45b8-804b-db9eb46191b2">

Penjelasan filter :
    
    1. tcp.dstport == 80 memeriksa apakah port tujuan (dstport) dari paket adalah 80 untuk protokol TCP.
    2. udp.dstport == 80 memeriksa apakah port tujuan (dstport) dari paket adalah 80 untuk protokol UDP.

    Dengan menggunakan filter tcp.port == 80 || udp.port == 80, kita akan menangkap semua paket yang ditujukan ke port 80, tanpa memandang protokol yang digunakan (TCP atau UDP). Ini memastikan bahwa kita tidak melewatkan paket yang mungkin menggunakan UDP pada port 80.

Flag yang kami peroleh untuk soal ini adalah sebagai berikut:

![soal8flag](https://github.com/rayrednet/Jarkom-Modul-1-B04-2023/assets/89269231/cced9258-71bb-4922-a718-9a348d8613fc)

#### Kendala yang dialami
Belum ditemukan kendala dalam pengerjaan soal nomor 8

### ⭐ Nomor 9
### Soal
Berikan kueri filter sehingga wireshark hanya mengambil paket yang berasal dari alamat 10.51.40.1 tetapi tidak menuju ke alamat 10.39.55.34!

### Jawaban:
#### Langkah Pengerjaan beserta Screenshot
Langkah-langkah yang telah kami terapkan untuk menyelesaikan tugas ini adalah sebagai berikut: <br />

Langkah pertama, untuk mengambil semua paket yang berasal dari alamat `10.51.40.1` tetapi tidak menuju ke alamat `10.39.55.34` adalah dengan memberikan filter expression `(ip.src == 10.51.40.1 && ip.dst != 10.39.55.34)`.

![soal9](https://github.com/rayrednet/Jarkom-Modul-1-B04-2023/assets/89269231/a69cd52a-0148-4c36-bd6d-fef85921503d)

Penjelasan filter :

    1. ip.src == 10.51.40.1: Kondisi pertama memeriksa apakah alamat sumber (ip.src) dari paket adalah 10.51.40.1. Ini berarti filter akan memilih paket-paket yang berasal dari alamat IP 10.51.40.1.
    2. ip.dst != 10.39.55.34: Kondisi kedua memeriksa apakah alamat tujuan (ip.dst) dari paket tidak sama dengan 10.39.55.34. Ini berarti filter akan membuang paket-paket yang menuju ke alamat IP 10.39.55.34

    Maka filter tersebut akan sesuai permintaan soal, namun tidak ada paket yang tertangkap menggunakan filter tersebut.

Flag yang kami peroleh untuk soal ini adalah sebagai berikut:

<img width="903" alt="image" src="https://github.com/rayrednet/Jarkom-Modul-1-B04-2023/assets/89933907/ffc23002-f362-4905-9c5b-696afbf2b097">


#### Kendala yang dialami

Belum ditemukan kendala dalam pengerjaan soal nomor 9

### ⭐ Nomor 10
### Soal
Sebutkan kredensial yang benar ketika user mencoba login menggunakan Telnet

### Jawaban:
#### Langkah Pengerjaan beserta Screenshot
Berikut ini adalah langkah-langkah yang kami lakukan untuk menyelesaikan soal ini: <br />

Telnet adalah protokol yang digunakan untuk mengakses dan mengendalikan perangkat jarak jauh melalui koneksi jaringan. Namun, Telnet mengirim data dalam teks terbuka (plaintext), yang berarti bahwa informasi seperti username dan password yang dimasukkan oleh pengguna tidak dienkripsi.

Langkah pertama, untuk menemukan kredensial pada soal ini kita gunakan filter `telnet contains "Password"` yang akan menghasilkan output sebagai berikut:

<img width="959" alt="image" src="https://github.com/rayrednet/Jarkom-Modul-1-B04-2023/assets/89933907/ead7b19b-2405-4214-92ab-dded49b9225f">

Filter tersebut digunakan dalam Wireshark untuk mencari kredensial (username dan password) yang mungkin terbuka dalam data paket saat pengguna mencoba login menggunakan protokol Telnet.

Langkah kedua, kita mencari kredensial dengan membuka melakukan follow TCP stream. Diperoleh hasil output sebagai berikut:

![image](https://github.com/rayrednet/Jarkom-Modul-1-B04-2023/assets/89933907/96e2fc2c-2587-4e29-8003-2fecdc0378c0)

Pada screenshot di atas, terlihat bahwa terdapat kredensial user yang berupa login dan password. Apabila kita perhatikan terdapat 2 warna di dalam stream tersebut, `warna merah menanadakan client` dan `warna biru menandakan server`. Untuk melihat kredensial, kita harus melihat secara khusus pada stream paket dari client, maka diperoleh sebagai berikut:

<img width="955" alt="image" src="https://github.com/rayrednet/Jarkom-Modul-1-B04-2023/assets/89933907/ce0471f4-e91c-41ea-adc4-d3e34717deb8">

Maka dari itu, kredensial user pada soal ini dengan format `username:password` adalah `dhafin:kesayangannyak0k0`


Flag yang kami peroleh untuk soal ini adalah sebagai berikut:

![soal10flag](https://github.com/rayrednet/Jarkom-Modul-1-B04-2023/assets/89269231/460a1c9d-9371-4c5d-94a7-62806bdd89a4)

#### Kendala yang dialami

Belum ditemukan kendala dalam pengerjaan soal nomor 10
