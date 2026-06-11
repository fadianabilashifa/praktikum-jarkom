# Laporan Praktikum Jaringan Komputer - Modul 9
## Web Server Multithreaded dan HTTP Client

---


### **Identitas Praktikan**
| Detail Mahasiswa | Informasi |
| :--- | :--- |
| **Nama** | [Fadia Nabila Shifa] |
| **NIM** | [103072400066] |
| **Kelas** | [IF-04-02] |


---

## 9.1 Tujuan Praktikum

1. Membuat web server sederhana menggunakan socket TCP.
2. Menerapkan konsep multithreading pada web server.
3. Memahami mekanisme HTTP request dan HTTP response.
4. Membuat program HTTP client tanpa bantuan browser.
5. Menguji komunikasi antara client dan server menggunakan protokol TCP.

---

## 9.2 Implementasi Web Server Multithreaded

### 9.2.1 Kode Program Server

**File:** `server.py`

```python
from socket import *
import threading

def handle_client(connectionSocket):
    try:
        message = connectionSocket.recv(1024).decode()
        filename = message.split()[1]

        f = open(filename[1:])
        outputdata = f.read()

        connectionSocket.send("HTTP/1.1 200 OK\r\n\r\n".encode())
        connectionSocket.send(outputdata.encode())

        connectionSocket.close()

    except:
        connectionSocket.send("HTTP/1.1 404 Not Found\r\n\r\n".encode())
        connectionSocket.close()

def main():
    serverSocket = socket(AF_INET, SOCK_STREAM)
    serverSocket.bind(('', 6789))
    serverSocket.listen(5)

    print("Server berjalan pada port 6789...")

    while True:
        connectionSocket, addr = serverSocket.accept()
        print("Client terhubung:", addr)

        thread = threading.Thread(target=handle_client, args=(connectionSocket,))
        thread.start()

if __name__ == "__main__":
    main()
```

### Penjelasan Program

- Server menggunakan socket TCP dengan tipe `SOCK_STREAM`.
- Fungsi `bind()` digunakan untuk menghubungkan server ke port 6789.
- `listen(5)` memungkinkan server menerima beberapa koneksi client.
- Setiap koneksi yang masuk akan diproses menggunakan thread yang berbeda.
- Server membaca file yang diminta client lalu mengirimkan HTTP response.
- Jika file tidak ditemukan, server mengirimkan pesan error 404.

---

### 9.2.2 Hasil Eksekusi Server

#### Menjalankan Server

```bash
python server.py
```

![Server](../assets/image/w9g1.png)

> Gambar menunjukkan server berhasil dijalankan pada port 6789 dan siap menerima koneksi dari client.

---

## 9.3 Implementasi HTTP Client

### 9.3.1 Kode Program Client

**File:** `client.py`

```python
import sys
from socket import *

server_host = sys.argv[1]
server_port = int(sys.argv[2])
filename = sys.argv[3]

clientSocket = socket(AF_INET, SOCK_STREAM)
clientSocket.connect((server_host, server_port))

request = f"GET /{filename} HTTP/1.1\r\nHost: {server_host}\r\n\r\n"
clientSocket.send(request.encode())

print("Response dari server:")

while True:
    data = clientSocket.recv(4096)
    if not data:
        break
    print(data.decode(), end="")

clientSocket.close()
```

### Penjelasan Program

- Client dibuat menggunakan socket TCP.
- Fungsi `connect()` digunakan untuk menghubungkan client ke server.
- Program mengirimkan HTTP GET request untuk meminta file tertentu.
- Response diterima menggunakan fungsi `recv()`.
- Isi response ditampilkan langsung pada terminal.

---

### 9.3.2 Hasil Eksekusi Client

#### Menjalankan Client

```bash
python client.py localhost 6789 index.html
```

![Client](../assets/image/w9g2.png)

> Gambar menunjukkan client berhasil mengirim request dan menerima response dari server berupa status 200 OK serta isi file HTML.

---

## 9.4 File HTML yang Digunakan

**File:** `index.html`

```html
<html>
<body>
<h1>Hello Server!</h1>
</body>
</html>
```

![HTML](../assets/image/w9g3.png)

> Gambar menunjukkan file HTML yang akan dikirimkan oleh server ketika diminta oleh client.

---

## 9.5 Analisis Praktikum

### 9.5.1 Analisis Web Server Multithreaded

#### Hasil Pengamatan

- Server dapat melayani beberapa client secara bersamaan.
- Setiap koneksi diproses pada thread yang berbeda.
- Server tetap responsif ketika menerima lebih dari satu request.

#### Keunggulan

- Kinerja server menjadi lebih baik saat melayani banyak client.
- Waktu tunggu client menjadi lebih singkat.
- Proses komunikasi berjalan lebih efisien.

#### Keterbatasan

- Membutuhkan resource sistem yang lebih besar.
- Terlalu banyak thread dapat mempengaruhi performa server.

---

### 9.5.2 Analisis HTTP Client

#### Hasil Pengamatan

- Client berhasil mengirimkan HTTP GET request ke server.
- Server memberikan response sesuai file yang diminta.
- Response terdiri dari header HTTP dan body berupa isi file.
- Komunikasi berlangsung menggunakan protokol TCP.

---

## 9.6 Pengujian Tambahan

### 9.6.1 Pengujian Multiple Client

#### Percobaan

Menjalankan beberapa client secara bersamaan untuk menguji kemampuan server dalam menangani banyak koneksi.

#### Hasil

- Semua client berhasil terhubung ke server.
- Server tetap berjalan dengan normal tanpa error.
- Setiap request diproses secara paralel melalui thread yang berbeda.

![Multiple Client](../assets/image/w9g4.png)

> Gambar menunjukkan beberapa client berhasil terhubung dan memperoleh response dari server secara bersamaan.

---

## 9.7 Kesimpulan

1. Web server sederhana berhasil dibuat menggunakan socket TCP.
2. Multithreading memungkinkan server menangani banyak client secara bersamaan.
3. HTTP client dapat mengirim request dan menerima response tanpa browser.
4. Response server terdiri dari header dan body sesuai format HTTP.
5. Konsep komunikasi client-server berhasil diterapkan dan dipahami melalui praktikum ini.

---