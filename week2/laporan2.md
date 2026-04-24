# Laporan Praktikum Jaringan Komputer - Modul 2
## Analisis Protokol Jaringan Menggunakan Wireshark

---

### **Identitas Praktikan**
| Detail Mahasiswa | Informasi |
| :--- | :--- |
| **Nama** | [Fadia Nabila Shifa] |
| **NIM** | [103072400066] |
| **Kelas** | [IF-04-02] |

---

### **1. Tujuan Praktikum**
Berdasarkan panduan praktikum Jaringan Komputer, sasaran utama dari pelaksanaan Modul 2 ini adalah:
1. Mahasiswa mampu melakukan persiapan serta instalasi perangkat lunak **Wireshark** secara mandiri.
2. Mahasiswa mampu mengoperasikan fitur-fitur utama Wireshark untuk melakukan penyadapan (*capturing*) dan identifikasi paket data pada jaringan aktif.

---

### **2. Landasan Teori**

#### **2.1 Mekanisme Kerja Packet Sniffer**
Wireshark dioperasikan sebagai *Packet Sniffer*, yakni sebuah instrumen yang berfungsi untuk mengamati pertukaran data antar entitas protokol secara pasif. Alat ini bekerja dengan menyalin setiap pesan yang melintasi antarmuka jaringan tanpa melakukan modifikasi atau intervensi terhadap arus data aslinya.

Fungsionalitas *Packet Sniffer* ditopang oleh dua pilar utama:
* **Capture Library:** Bertugas mengamankan salinan dari setiap *frame* pada lapisan fisik yang dideteksi oleh perangkat.
* **Packet Analyzer:** Bertugas menguraikan seluruh *field* dalam pesan protokol berdasarkan standar yang berlaku (seperti Ethernet, IP, TCP, dan HTTP).

#### **2.2 Organisasi Antarmuka Wireshark**
Lingkungan kerja Wireshark didukung oleh lima komponen fungsional utama:
1. **Command Menu:** Kumpulan navigasi untuk mengelola seluruh operasional aplikasi.
2. **Packet Listing:** Daftar ringkas seluruh paket yang berhasil diakuisisi secara kronologis.
3. **Packet Header Details:** Penjelasan mendalam mengenai lapisan protokol paket yang dipilih secara hierarkis.
4. **Packet Contents:** Tampilan konten mentah dari sebuah *frame* dalam format ASCII dan heksadesimal.
5. **Display Filter Field:** Kolom khusus untuk menyaring paket data guna meningkatkan efisiensi analisis.

---

### **3. Prosedur Pelaksanaan**

Berikut adalah urutan prosedur sistematis yang dilaksanakan selama praktikum:

1. **Tahap Inisialisasi:** Memastikan koneksi internet aktif, lalu menjalankan aplikasi peramban serta perangkat lunak Wireshark.
2. **Aktivasi Capturing:** Memilih *interface* jaringan yang aktif (misal: Wi-Fi) melalui menu `Capture` > `Interfaces`, kemudian menekan instruksi **Start**.
3. **Pemicuan Traffic:** Mengakses laman web pengujian `http://gaia.cs.umass.edu/wireshark-labs/INTRO-wireshark-file1.html` dan menunggu hingga konten termuat sepenuhnya.
4. **Terminasi dan Filtrasi:** Menghentikan proses perekaman (tombol kotak merah), lalu menggunakan filter `http` untuk mengisolasi paket yang relevan.
5. **Analisis Struktur:** Membedah paket `HTTP GET` melalui panel *Header Details* untuk menelaah enkapsulasi pada tiap lapisan protokol.

---

### **4. Analisis Hasil Pengamatan**

#### **4.1 Konfigurasi Interface Jaringan**
Pada tahap awal, aplikasi Wireshark dijalankan untuk mendeteksi seluruh antarmuka jaringan yang aktif pada perangkat. Pemilihan difokuskan pada *interface* yang menunjukkan grafik aktivitas trafik (seperti Wi-Fi) guna memastikan paket data dari aktivitas browsing dapat ditangkap dengan sempurna.
![Tampilan Awal](../assets/image/WelcomeScreen.png)

#### **4.2 Proses Akuisisi Paket Data (Capturing)**
Setelah memilih antarmuka yang tepat, proses *capture* dimulai berbarengan dengan pengaksesan URL target. Seluruh log lalu lintas data yang masuk dan keluar dari perangkat terekam secara kronologis, mencakup berbagai macam protokol yang berjalan di latar belakang sistem.
![capture](../assets/image/interfcecapture.png)

#### **4.3 Observasi Alamat IP (Source & Destination)**
Berdasarkan hasil tangkapan, dilakukan identifikasi terhadap alamat IP sumber (*Source*) dan alamat IP tujuan (*Destination*). Hal ini penting untuk memastikan bahwa paket yang dianalisis memang berasal dari perangkat lokal menuju ke server web target yang sedang diakses.
![packet](../assets/image/Packetlist.png)

**Penjelasan Hierarki Paket:**
* **Frame:** Informasi fisik mengenai paket yang diakuisisi.
* **Ethernet II:** Detail alamat fisik (MAC Address) sumber dan tujuan.
* **Internet Protocol Version 4:** Informasi alamat logika (IP Address) pengirim dan penerima.
* **Transmission Control Protocol:** Mengelola informasi *port* serta sinkronisasi nomor urut paket.
* **Hypertext Transfer Protocol:** Memuat metode *request* (GET), identitas *host*, dan informasi *user-agent*.

#### **4.4 Implementasi Display Filter HTTP**
Mengingat banyaknya paket yang terekam, diterapkan filter spesifik dengan kata kunci `http`. Langkah ini bertujuan untuk menyaring trafik dan hanya menampilkan paket yang relevan dengan protokol lapisan aplikasi, sehingga mempermudah proses audit data.
![http](../assets/image/http.png)

#### **4.5 Dekomposisi Struktur Protokol HTTP GET**
Melalui panel *Packet Header Details*, dilakukan analisis mendalam terhadap struktur paket **HTTP GET**. Hirarki enkapsulasi data dapat diuraikan sebagai berikut:
* **Frame:** Informasi fisik paket pada lapisan data link.
* **Ethernet II:** Memuat detail alamat fisik (MAC Address) pengirim dan penerima.
* **Internet Protocol Version 4:** Menyediakan informasi alamat logika (IP Address) sumber dan tujuan.
* **Transmission Control Protocol (TCP):** Mengatur mekanisme transport, termasuk *port* dan nomor urut paket.
* **Hypertext Transfer Protocol:** Berisi instruksi aplikasi seperti metode `GET`, alamat *host*, dan tipe *browser* yang digunakan.
![get](../assets/image/httpget.png)

#### **4.6 Representasi Data Mentah (Hex & ASCII)**
Bagian terakhir adalah tinjauan pada panel *Packet Bytes*. Di sini, isi asli dari paket disajikan dalam format heksadesimal dan karakter ASCII. Tampilan ini memungkinkan kita untuk melihat data mentah yang sebenarnya dikirimkan melalui jaringan sebelum diterjemahkan oleh sistem.
![packet](../assets/image/tampilanpaket.png)

---

---

### **5. Kesimpulan**
Berdasarkan hasil observasi dan analisis yang telah dilakukan, dapat disimpulkan beberapa poin utama sebagai berikut:
1. **Efektivitas Tools:** Wireshark terbukti sebagai instrumen *packet sniffer* yang andal dalam memetakan dinamika komunikasi data pada jaringan secara *real-time*.
2. **Krusialitas Fitur Filter:** Penggunaan *display filter* sangat krusial untuk menyaring redundansi paket, sehingga proses identifikasi protokol spesifik (seperti HTTP) menjadi lebih efisien.
3. **Interdependensi Protokol:** Terlihat adanya keterkaitan antar-layer, di mana operasional lapisan aplikasi (HTTP) sepenuhnya ditopang oleh protokol lapisan bawah seperti TCP, IP, dan Ethernet.
4. **Kompetensi Analisis:** Praktikum ini berhasil memperkuat pemahaman mengenai struktur enkapsulasi data serta navigasi antarmuka Wireshark sebagai landasan analisis jaringan tingkat lanjut.