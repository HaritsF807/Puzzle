# PuzzleCam — Gesture Capture

Aplikasi photobooth yang dikontrol sepenuhnya menggunakan gestur tangan secara langsung di browser Anda. Tanpa instalasi backend, tanpa database, dan tanpa dependensi lokal yang perlu dipasang.

---

## **DESKRIPSI**

PuzzleCam mengambil foto dengan mendeteksi kedua tangan Anda sebagai "bingkai" foto, mengubah gambar tersebut menjadi puzzle 3x3 dengan efek foto hitam-putih (photobooth retro), dan memungkinkan Anda menyusunnya kembali menggunakan gestur mencubit (*pinch*). Setelah puzzle selesai disusun, foto dapat disimpan ke dalam galeri samping dan digabungkan menjadi strip foto (*photo strip*) yang dapat diunduh.

---

## **PERSYARATAN SISTEM**

- **Browser:** Chrome o Edge (sangat disarankan), Firefox
- **Hardware:** Webcam / Kamera Web
- **Koneksi Internet:** Diperlukan untuk memuat model pendeteksi tangan MediaPipe (~10MB, hanya saat pertama kali dibuka)
- **Server Lokal:** Diperlukan untuk menjalankan aplikasi (tidak dapat dibuka langsung sebagai berkas `file://` lokal di browser)

---

## **INSTALASI DAN KONFIGURASI**

### 1. Clone Repositori

```bash
git clone https://github.com/HaritsF807/Puzzle.git
cd Puzzle
```

### 2. Jalankan Server Lokal

Aplikasi menggunakan modul ES dan memerlukan akses kamera, sehingga harus dijalankan melalui protokol HTTP.

* Jika menggunakan **VS Code**, pasang ekstensi [Live Server](https://marketplace.visualstudio.com/items?itemName=ritwickdey.LiveServer) dan klik tombol **Go Live** di bagian pojok kanan bawah.
* Jika menggunakan **Laragon**, Anda dapat meletakkannya di direktori `C:\laragon\www\Puzzle` lalu membukanya di browser.

### 3. Buka di Browser

```text
http://localhost:5500
```
Berikan izin akses kamera saat diminta oleh browser Anda.

---

## **STRUKTUR PROYEK**

```text
Puzzle/
├── index.html        # Halaman utama aplikasi (UI)
├── app.js            # Logika utama (webcam, pelacakan gestur, puzzle, galeri)
├── css/
│   └── styles.css    # Penataan layout dan gaya visual (CSS)
└── .gitignore
```

---

## **GESTUR KONTROL**

| Gestur | Aksi / Fungsi |
|---|---|
| **Mencubit dengan kedua tangan (`pinch`)** | Mengunci area bingkai tangan dan langsung mengambil foto secara instan |
| **Mencubit dengan satu tangan (`pinch`) di atas kepingan** | Menyeret (*drag*) kepingan puzzle ke posisi yang benar |
| **Kepalan tangan (`fist`) (tahan)** | Menyimpan puzzle yang telah selesai disusun ke galeri / Reset papan puzzle |

---

## **ALUR LOGIKA APLIKASI**

1. Tunjukkan kedua tangan Anda ke kamera dan lakukan gerakan cubit (`pinch`) untuk menentukan area bingkai foto.
2. Tahan cubitan tersebut selama `250ms` — foto akan langsung diambil secara otomatis secara instan.
3. Gambar yang diambil akan dibagi menjadi kepingan puzzle 3x3 dengan efek foto hitam-putih retro.
4. Susun kembali kepingan puzzle tersebut menggunakan gerakan cubit (`pinch`) satu tangan untuk menggesernya.
5. Setelah puzzle selesai disusun, buat gerakan mengepalkan tangan (`fist`) untuk memicu efek pemecahan (*shatter*) dan menyimpannya ke strip foto.
6. Anda dapat mengunduh strip foto lengkap setelah mengumpulkan maksimal 3 foto di galeri.

---

## **TEKNOLOGI YANG DIGUNAKAN**

- **[MediaPipe Tasks Vision](https://developers.google.com/mediapipe)** `v0.10.14` — Untuk mendeteksi koordinat titik-titik tangan (*landmarks*) secara real-time.
- **Canvas 2D API** — Untuk pemrosesan gambar, pembagian kepingan puzzle, dan filter hitam-putih photobooth.
- **JavaScript (ES Modules)** — Logika pemrograman murni tanpa framework (*Vanilla JS*).
- **CSS Custom Properties** — Untuk penataan layout responsif dan tema gelap modern.

Semua pustaka pihak ketiga dimuat melalui CDN, sehingga tidak memerlukan instalasi lokal tambahan.

---

## **PANDUAN PENYELESAIAN MASALAH**

### **Kamera Tidak Menyala**
Pastikan tidak ada aplikasi lain (seperti Teams, Zoom, Discord, dll.) yang sedang menggunakan kamera di latar belakang.

### **Model MediaPipe Gagal Dimuat**
Periksa koneksi internet Anda. Model MediaPipe (~10MB) diunduh secara dinamis dari `storage.googleapis.com` dan pustaka runtime dari `cdn.jsdelivr.net`. Jika domain tersebut diblokir oleh jaringan Anda, aplikasi tidak akan bisa dimuat.

### **Halaman Layar Hitam**
Pastikan Anda membuka aplikasi melalui server lokal dengan protokol HTTP (misal: `http://localhost:5500`), bukan dengan cara mendobel klik berkas `index.html` langsung dari File Explorer (protokol `file://`).

### **Gestur Pinch Tidak Terdeteksi**
Pastikan pencahayaan ruangan cukup terang dan kedua tangan Anda berada dalam jangkauan pandangan kamera. Dekatkan jari telunjuk dan ibu jari Anda hingga indikator lingkaran kuning di layar menyala aktif.

---

## **LISENSI**

MIT — Bebas untuk digunakan, dimodifikasi, dan dibagikan.
