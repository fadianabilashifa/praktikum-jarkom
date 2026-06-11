# Laporan Praktikum Jaringan Komputer - Modul 13
## Analisis Ethernet dan Address Resolution Protocol (ARP) Menggunakan Wireshark

---


### **Identitas Praktikan**
| Detail Mahasiswa | Informasi |
| :--- | :--- |
| **Nama** | [Fadia Nabila Shifa] |
| **NIM** | [103072400066] |
| **Kelas** | [IF-04-02] |


---

# Pendahuluan

Ethernet merupakan teknologi jaringan yang bekerja pada lapisan Data Link (Layer 2) dalam model OSI. Teknologi ini digunakan untuk mengirimkan data dalam bentuk frame antar perangkat yang berada dalam jaringan lokal (LAN).

Dalam proses komunikasi jaringan, perangkat tidak hanya membutuhkan alamat IP tetapi juga alamat fisik atau MAC Address. Untuk itu digunakan Address Resolution Protocol (ARP), yaitu protokol yang berfungsi menerjemahkan alamat IP menjadi MAC Address sehingga data dapat dikirim ke perangkat tujuan dengan benar.

Pada praktikum ini dilakukan pengamatan terhadap frame Ethernet dan proses ARP menggunakan aplikasi Wireshark. Selain itu, dilakukan pemeriksaan ARP Cache melalui Command Prompt untuk melihat daftar pemetaan alamat IP dan MAC Address yang tersimpan pada komputer.

Melalui praktikum ini diharapkan mahasiswa dapat memahami proses komunikasi pada layer Data Link serta peran ARP dalam mendukung komunikasi jaringan.

---

# Tujuan Praktikum

1. Memahami konsep dasar Ethernet pada jaringan komputer.
2. Mengetahui fungsi dan mekanisme kerja ARP.
3. Menggunakan Wireshark untuk menangkap dan menganalisis frame Ethernet.
4. Mengamati isi ARP Cache yang tersimpan pada komputer.
5. Menganalisis proses ARP Request dan ARP Reply dalam jaringan.

---

# Tools yang Digunakan

| Tools | Fungsi |
|--------|--------|
| Wireshark | Melakukan capture dan analisis paket jaringan |
| Command Prompt | Menjalankan perintah ARP |
| Sistem Operasi Windows | Lingkungan praktikum |

---

# Langkah-Langkah Praktikum

## 1. Menangkap dan Menganalisis Frame Ethernet

Langkah pertama dilakukan dengan membuka aplikasi Wireshark dan memilih interface jaringan yang aktif. Setelah proses capture dimulai, dilakukan aktivitas jaringan sehingga paket yang melewati interface dapat direkam.

Selanjutnya salah satu frame Ethernet dipilih untuk dianalisis. Informasi yang dapat diamati meliputi Source MAC Address, Destination MAC Address, dan EtherType yang menunjukkan jenis protokol yang dibawa oleh frame tersebut.

Masukkan URL berikut ke browser:

```text
http://gaia.cs.umass.edu/wireshark-labs/HTTP-ethereal-lab-file3.html
```

![Gambar 1](../assets/image/w13g1.png)

> Menunjukkan proses membuka URL yang digunakan selama praktikum dan hasil capture pada Wireshark.

### Hasil Analisis Frame Ethernet

![Gambar 2](../assets/image/w13g2.png)

> Menunjukkan detail frame Ethernet yang berhasil dianalisis menggunakan Wireshark.

---

## 2. Melihat Isi ARP Cache

Untuk melihat daftar alamat IP dan MAC Address yang tersimpan pada komputer, Command Prompt dibuka kemudian dijalankan perintah berikut:

```bash
arp -a
```

Perintah tersebut digunakan untuk menampilkan ARP Cache yang berisi informasi hasil pemetaan antara alamat IP dan MAC Address yang telah dikenali oleh sistem.

### Hasil Perintah ARP

![Gambar 3](../assets/image/w13g3.png)

> Menunjukkan hasil eksekusi perintah `arp -a` yang menampilkan isi ARP Cache pada komputer.

---

## 3. Mengamati Paket ARP Menggunakan Wireshark

Setelah melihat isi ARP Cache, dilakukan pengamatan terhadap paket ARP yang berhasil ditangkap oleh Wireshark.

Dari hasil capture dapat diamati proses pencarian alamat fisik perangkat melalui ARP Request dan balasan yang diberikan melalui ARP Reply.

### Hasil Capture Paket ARP

![Gambar 4](../assets/image/w13g4.png)

> Menunjukkan paket ARP yang berhasil direkam dan dianalisis menggunakan Wireshark.

---

# Hasil dan Analisis

## 1. Analisis Frame Ethernet

Berdasarkan hasil pengamatan pada Wireshark, frame Ethernet memiliki beberapa komponen utama yaitu:

- Destination MAC Address
- Source MAC Address
- EtherType

Destination MAC Address menunjukkan alamat fisik perangkat tujuan, sedangkan Source MAC Address menunjukkan alamat fisik perangkat pengirim. Sementara itu, EtherType digunakan untuk mengidentifikasi protokol yang dibawa oleh frame, seperti IPv4, IPv6, atau ARP.

Frame Ethernet berperan sebagai unit data utama yang digunakan untuk komunikasi pada layer Data Link.

---

## 2. Analisis ARP Cache

Hasil perintah `arp -a` menunjukkan daftar pasangan alamat IP dan MAC Address yang tersimpan pada komputer.

ARP Cache berfungsi sebagai penyimpanan sementara hasil pemetaan alamat sehingga komputer tidak perlu melakukan pencarian ulang setiap kali ingin berkomunikasi dengan perangkat yang sama. Dengan adanya cache ini, proses komunikasi menjadi lebih cepat dan efisien.

---

## 3. Analisis Paket ARP

Dari hasil capture Wireshark dapat diamati bahwa ARP bekerja menggunakan dua jenis pesan utama.

### ARP Request

ARP Request dikirim secara broadcast ke seluruh perangkat dalam jaringan lokal untuk mencari MAC Address yang sesuai dengan alamat IP tertentu.

Tujuan dari pesan ini adalah menanyakan perangkat mana yang memiliki alamat IP yang dicari oleh pengirim.

### ARP Reply

ARP Reply dikirim oleh perangkat yang memiliki alamat IP tersebut sebagai respons terhadap ARP Request.

Pesan ini berisi informasi MAC Address yang dimiliki oleh perangkat tujuan sehingga pengirim dapat melakukan komunikasi secara langsung.

Setelah menerima ARP Reply, hasil pemetaan tersebut akan disimpan ke dalam ARP Cache untuk digunakan pada komunikasi berikutnya.

---

# Kesimpulan

1. Ethernet merupakan teknologi jaringan pada layer Data Link yang digunakan untuk mengirimkan data dalam bentuk frame antar perangkat dalam jaringan lokal.
2. ARP berfungsi untuk menerjemahkan alamat IP menjadi MAC Address sehingga komunikasi antar perangkat dapat berlangsung dengan benar.
3. Wireshark berhasil digunakan untuk menangkap dan menganalisis frame Ethernet serta paket ARP yang melintas pada jaringan.
4. Hasil pengamatan menunjukkan bahwa proses ARP berlangsung melalui tahapan ARP Request dan ARP Reply.
5. Praktikum ini membantu memahami komunikasi pada layer Data Link serta mekanisme pemetaan alamat yang dilakukan oleh ARP.

---