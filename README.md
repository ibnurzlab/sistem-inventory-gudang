# GudangPro — Sistem Inventory & Gudang Sederhana

![HTML5](https://img.shields.io/badge/HTML5-E34F26?style=flat-square&logo=html5&logoColor=white)
![Tailwind CSS](https://img.shields.io/badge/Tailwind_CSS-06B6D4?style=flat-square&logo=tailwindcss&logoColor=white)
![JavaScript](https://img.shields.io/badge/JavaScript-F7DF1E?style=flat-square&logo=javascript&logoColor=black)
![Tanpa Build](https://img.shields.io/badge/build-tanpa_build_step-22c55e?style=flat-square)
[![Demo Online](https://img.shields.io/badge/demo-online-3b82f6?style=flat-square&logo=githubpages&logoColor=white)](https://ibnurzlab.github.io/sistem-inventory-gudang/)
![Lisensi](https://img.shields.io/badge/lisensi-MIT-blue?style=flat-square)

Sistem inventory dan manajemen gudang berbasis web yang **ringan, tanpa instalasi, dan tanpa backend**. Cukup satu file `index.html`, seluruh data tersimpan otomatis di **localStorage** browser sehingga aplikasi dapat dipakai sepenuhnya secara offline.

Dirancang untuk kebutuhan gudang skala kecil–menengah: pencatatan stok, mutasi barang masuk/keluar, peringatan stok menipis, laporan valuasi aset, dan ekspor ke CSV/Excel.

---

## 🔗 Demo Langsung

**https://ibnurzlab.github.io/sistem-inventory-gudang/**

Masuk menggunakan salah satu akun demo berikut:

| Peran | Username | Kata Sandi |
| :--- | :--- | :--- |
| Admin | `admin` | `admin123` |
| Staf Gudang | `staf` | `staf123` |

> Demo ini berjalan sepenuhnya di browser Anda — data yang Anda input hanya tersimpan di perangkat sendiri dan tidak dikirim ke mana pun.

---

## 📑 Daftar Isi

- [Fitur Utama](#-fitur-utama)
- [Demo Langsung](#-demo-langsung)
- [Autentikasi & Peran Pengguna](#-autentikasi--peran-pengguna)
- [Teknologi](#-teknologi)
- [Struktur Proyek](#-struktur-proyek)
- [Cara Menjalankan](#-cara-menjalankan)
- [Alur Penggunaan](#-alur-penggunaan)
- [Struktur Data (localStorage)](#-struktur-data-localstorage)
- [Ekspor Data](#-ekspor-data)
- [Catatan Keamanan](#-catatan-keamanan)
- [Roadmap](#-roadmap)
- [Lisensi](#-lisensi)

---

## ✨ Fitur Utama

### 🔐 Autentikasi & Sesi
- Halaman login wajib sebelum masuk ke aplikasi.
- Kata sandi **tidak disimpan sebagai teks polos** — disimpan sebagai **hash SHA-256 + salt unik** per akun.
- Pembatasan percobaan: salah **5×** → login dikunci **30 detik** dengan penghitung waktu.
- **"Ingat saya"** (sesi 7 hari di `localStorage`) atau sesi biasa (8 jam di `sessionStorage`).
- Deteksi sesi kedaluwarsa otomatis + pemantau sesi berkala.
- Fitur **Ganti Kata Sandi** dengan verifikasi sandi lama.
- Hak akses berbasis peran: reset data hanya untuk **Admin**.

### 📊 Dashboard
- Kartu metrik: total jenis item (SKU), total kuantitas fisik, estimasi nilai stok, dan jumlah item yang perlu reorder.
- Tabel **stok menipis** dengan tombol aksi cepat "+ Tambah Stok".
- Daftar **5 transaksi terakhir**.
- Panduan alur kerja 4 langkah untuk staf baru.

### 📦 Master Barang (CRUD)
- Tambah, ubah, dan hapus data barang.
- Validasi **SKU unik**, harga & stok tidak boleh negatif.
- Pencarian nama/SKU dan filter per kategori.
- Status otomatis: **Aman** atau **Menipis** berdasarkan batas minimum stok.
- Stok awal yang diisi saat input barang otomatis tercatat sebagai transaksi masuk ("Stok Awal Sistem").

### ⬇️⬆️ Barang Masuk & Barang Keluar
- Form penerimaan: barang, jumlah, supplier, tanggal, catatan.
- Form pengeluaran: barang, jumlah, tujuan/pelanggan, tanggal, catatan.
- **Validasi stok**: pengeluaran melebihi stok akan ditolak, stok tidak pernah minus.
- Info stok tersedia muncul langsung saat memilih barang.
- Riwayat 10 transaksi masuk / keluar terbaru.

### 🕓 Riwayat Stok
- Log seluruh mutasi stok (masuk & keluar) dengan pencarian teks bebas.
- Filter kombinasi: barang, jenis transaksi, dan tanggal spesifik.
- Penghitung hasil filter: "Menampilkan X dari total Y transaksi".

### 📈 Laporan & Ekspor
- Ringkasan agregat per kategori (jumlah SKU, total unit, nilai).
- Tabel valuasi inventaris lengkap dengan subtotal dan status stok.
- Ekspor **CSV Stok Barang** dan **CSV Semua Transaksi** (UTF-8 + BOM, aman dibuka di Excel).

### 🧩 Pengalaman Pengguna
- Antarmuka responsif (mobile & desktop) dengan sidebar yang dapat dibuka-tutup.
- Notifikasi *toast* untuk setiap aksi berhasil/gagal.
- Modal dapat ditutup dengan tombol **ESC**.
- Data contoh siap pakai (10 barang + 7 transaksi) dan tombol "Reset Data Awal".
- Semua data yang ditampilkan sudah di-escape untuk mencegah XSS.

---

## 👤 Autentikasi & Peran Pengguna

Aplikasi otomatis membuat dua akun bawaan saat pertama kali dibuka:

| Peran | Username | Kata Sandi | Hak Akses |
| :--- | :--- | :--- | :--- |
| **Admin** | `admin` | `admin123` | Semua fitur + Reset Data Awal |
| **Staf Gudang** | `staf` | `staf123` | Operasional gudang & laporan |

> ⚠️ **Segera ganti kata sandi bawaan** melalui menu **Ganti Sandi** di sidebar setelah login pertama.
> Pada layar login tersedia tombol **akun demo** untuk mengisi kredensial secara otomatis.

---

## 🛠 Teknologi

| Komponen | Keterangan |
| :--- | :--- |
| **HTML5** | Struktur aplikasi single-page |
| **Tailwind CSS** | Styling via CDN (utility-first, tanpa build) |
| **JavaScript (ES6+)** | Seluruh logika aplikasi, tanpa framework |
| **Lucide Icons** | Ikon SVG via CDN |
| **Web Crypto API** | Hashing SHA-256 kata sandi (dengan fallback) |
| **localStorage & sessionStorage** | Penyimpanan data & sesi di sisi klien |

Tidak ada `npm install`, tidak ada proses build, dan tidak ada server yang dibutuhkan.

---

## 📁 Struktur Proyek

```
sistem-inventory-gudang/
├── index.html      # Aplikasi lengkap (markup + styling + logika)
├── README.md       # Dokumentasi ini
├── LICENSE         # Lisensi MIT
└── .gitignore
```

Aplikasi sengaja dibuat dalam **satu file** agar mudah dibagikan, dipindahkan, dan dijalankan di komputer mana pun tanpa dependensi.

---

## 🚀 Cara Menjalankan

### Opsi 1 — Langsung (paling cepat)
Klik dua kali `index.html`, atau seret file tersebut ke jendela browser.

### Opsi 2 — Server lokal (disarankan)
Beberapa browser membatasi fitur tertentu pada protokol `file://`, jadi menjalankan lewat server lokal lebih ideal:

```bash
# Python 3
python -m http.server 8000

# Node.js
npx serve .
```

Lalu buka `http://localhost:8000`.

### Opsi 3 — VS Code
Gunakan ekstensi **Live Server** → klik kanan `index.html` → *Open with Live Server*.

> 📶 Koneksi internet diperlukan untuk memuat **Tailwind CSS**, **Lucide Icons**, dan **Google Fonts** dari CDN. Seluruh data tetap tersimpan lokal di browser.

---

## 🔄 Alur Penggunaan

1. **Master Barang** — daftarkan SKU, nama, kategori, satuan, harga, dan batas minimum stok.
2. **Barang Masuk** — catat kiriman dari supplier; stok bertambah otomatis.
3. **Barang Keluar** — catat pengeluaran untuk pesanan/pemakaian internal; stok berkurang dengan validasi otomatis.
4. **Pantau & Laporan** — cek item yang menipis di dashboard, lalu ekspor data ke CSV kapan saja.

---

## 🗄 Struktur Data (localStorage)

| Kunci | Isi |
| :--- | :--- |
| `gudang_items` | Daftar barang master |
| `gudang_txs` | Riwayat seluruh transaksi |
| `gudang_users` | Akun pengguna (username, nama, peran, salt, hash) |
| `gudang_session` | Sesi login aktif (masa berlaku, tanggal login) |
| `gudang_login_attempts` | Penghitung percobaan login gagal & waktu kunci |

**Contoh objek barang**

```json
{
  "id": "item_1",
  "sku": "BRG-ELK-01",
  "name": "Barcode Scanner Wireless 2D",
  "category": "Elektronik",
  "unit": "Unit",
  "price": 450000,
  "stock": 12,
  "minStock": 5
}
```

**Contoh objek transaksi**

```json
{
  "id": "tx_1",
  "type": "IN",
  "itemId": "item_1",
  "itemName": "Barcode Scanner Wireless 2D",
  "itemSku": "BRG-ELK-01",
  "qty": 10,
  "party": "PT Digital Solusindo",
  "date": "2025-05-10",
  "notes": "PO-2025-081 Pengadaan baru"
}
```

`type` bernilai `IN` untuk barang masuk dan `OUT` untuk barang keluar.

---

## 📤 Ekspor Data

Semua ekspor dihasilkan dalam format **CSV** yang dapat langsung dibuka di Microsoft Excel, Google Sheets, atau LibreOffice Calc:

- **CSV Stok Barang** — SKU, nama, kategori, satuan, harga, stok, batas minimum, subtotal nilai, dan status.
- **CSV Semua Transaksi** — ID transaksi, tanggal, jenis, SKU, nama barang, pihak terkait, jumlah, dan catatan.

---

## 🛡 Catatan Keamanan

Proyek ini adalah aplikasi **front-end murni** (tanpa backend), sehingga autentikasinya berjalan di sisi browser:

- Login berfungsi untuk **membatasi akses antar pengguna/staf** di perangkat yang sama.
- Kata sandi sudah di-hash, namun **bukan pengganti autentikasi server**. Data tetap dapat dilihat melalui DevTools dan dapat dihapus dengan membersihkan data browser.
- Untuk kebutuhan produksi/multi-perangkat, diperlukan backend + database + autentikasi berbasis token (JWT/session) dan HTTPS.

Jangan gunakan aplikasi ini untuk menyimpan data sensitif/rahasia tanpa menambahkan backend terlebih dahulu.

---

## 🗺 Roadmap

- [ ] Backend + database (Node.js/Express + SQLite/PostgreSQL)
- [ ] Autentikasi JWT & sinkronisasi multi-perangkat
- [ ] Barcode scanner / input scan SKU
- [ ] Grafik tren stok masuk & keluar
- [ ] Multi-gudang / multi-lokasi
- [ ] Cetak surat jalan & faktur (PDF)
- [ ] Mode gelap (dark mode)
- [ ] PWA + dukungan offline penuh (service worker)

---

## 🤝 Kontribusi

Kontribusi dan masukan sangat diterima:

1. *Fork* repository ini
2. Buat branch fitur (`git checkout -b fitur/fitur-baru`)
3. *Commit* perubahan (`git commit -m "Menambah fitur baru"`)
4. *Push* ke branch (`git push origin fitur/fitur-baru`)
5. Buka *Pull Request*

---

## 📄 Lisensi

Dirilis dengan lisensi **MIT** — bebas digunakan, dimodifikasi, dan didistribusikan. Lihat berkas [LICENSE](LICENSE) untuk detail.

---

## 👨‍💻 Penulis

**Ibnu Rizky** — [@ibnurzlab](https://github.com/ibnurzlab)

Dibuat sebagai proyek pembelajaran sekaligus alat bantu pencatatan stok gudang sehari-hari.
