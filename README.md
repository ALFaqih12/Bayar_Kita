# BayarKita — Aplikasi Pembayaran Tagihan & Pengisian Pulsa

> Aplikasi web frontend yang mensimulasikan pembayaran tagihan rutin (PLN, PDAM, Internet, Seminar), biaya kuliah/SPP, serta pengisian pulsa dan paket data. Dibangun dengan HTML, CSS (Tailwind), dan Vanilla JavaScript. Semua data disimpan di `localStorage` sehingga tidak memerlukan server atau database.

---

## 📋 Daftar Isi

- [Deskripsi](#deskripsi)
- [Fitur Utama](#fitur-utama)
- [Teknologi yang Digunakan](#teknologi-yang-digunakan)
- [Cara Menjalankan](#cara-menjalankan)
- [Struktur Data Dummy](#struktur-data-dummy)
- [Panduan Penggunaan](#panduan-penggunaan)
- [Pengembang](#pengembang)

---

## Deskripsi

**BayarKita** adalah aplikasi berbasis web yang dirancang untuk memudahkan pengguna dalam melakukan simulasi pembayaran berbagai tagihan dan pengisian pulsa. Aplikasi ini sepenuhnya berjalan di sisi klien (client-side) dan menggunakan `localStorage` untuk menyimpan riwayat transaksi. Dengan antarmuka yang modern dan responsif (mobile-first), aplikasi ini memberikan pengalaman yang intuitif dan interaktif.

---

## Fitur Utama

### 1. Dashboard / Beranda

- Ringkasan saldo wallet (simulasi) dengan detail pemasukan dan pengeluaran.
- Tombol aksi cepat: **Top Up** dan **Transfer**.
- Grid layanan: PLN, PDAM, Internet, Seminar → klik untuk navigasi cepat ke halaman bayar.
- Banner promo dengan tombol klaim.
- Tagihan mendesak dengan tombol "Bayar Sekarang" (otomatis mengisi nomor pelanggan).
- Aktivitas terbaru (3 transaksi terakhir).

### 2. Bayar Tagihan

- Pilihan kategori: **PLN**, **PDAM**, **Internet**, **Seminar**.
- Input nomor pelanggan (validasi: minimal 8 digit angka; untuk Seminar alfanumerik).
- Tombol **"Cek Tagihan"** → menampilkan data tagihan dummy (nama, alamat/periode, jumlah, denda, jatuh tempo).
- Tiga metode pembayaran:
  - **Virtual Account** → generate nomor VA unik.
  - **QRIS** → tampilkan QR code simulasi (dengan countdown 5 menit).
  - **Teller / Kasir** → tampilkan kode pembayaran dan daftar lokasi.
- Tombol **"Bayar Sekarang"** → loading state, modal bukti pembayaran (struk) yang dapat dicetak.
- Transaksi otomatis tersimpan di `localStorage`.

### 3. Biaya Kuliah / SPP

- Input NIM (validasi angka minimal 6 digit).
- Tombol **"Lihat Tagihan Semester"** → menampilkan daftar cicilan (6–8 item per semester) dengan status Lunas / Belum Lunas.
- Centang cicilan yang ingin dibayar → total otomatis terhitung.
- Menampilkan **Kode Tagihan** ringkasan (NIM, semester, jumlah cicilan belum lunas).
- Tombol **"Bayar Cicilan Terpilih"** → proses pembayaran dengan Virtual Account, update status menjadi Lunas (simulasi), dan muncul struk.

### 4. Isi Pulsa & Paket Data

- Pilih provider dari grid: Telkomsel, XL, Indosat, Tri (3), Smartfren, Axis.
- Input nomor HP (validasi 10–13 digit, diawali 08) → deteksi provider otomatis dari prefix.
- Pilih nominal pulsa: Rp10k, Rp25k, Rp50k, Rp100k, Rp200k, atau **Custom**.
- Pilihan paket data: 1GB, 3GB, 5GB, 10GB (opsional).
- Tombol **"Lanjutkan Pembayaran"** → loading, muncul modal bukti pembayaran dengan detail transaksi dan nomor VA.

### 5. Riwayat Transaksi

- Tabel histori semua transaksi yang tersimpan di `localStorage`.
- Filter berdasarkan kategori: Semua, PLN, PDAM, Internet, Seminar, SPP, Pulsa.
- Tombol **"Hapus Semua"** untuk membersihkan riwayat.
- Statistik: total transaksi dan total pengeluaran.

### 6. Fitur Pendukung

- **Responsif Mobile-First** – tampilan optimal di berbagai ukuran layar.
- **Bottom Navigation** – akses cepat ke halaman utama.
- **Notifikasi (Toast)** – sukses, error, warning, info.
- **Loading State** – spinner saat proses cek tagihan, bayar, atau cek NIM.
- **Modal & Struk** – tampilan bukti pembayaran dengan tombol cetak (`window.print()`).
- **Validasi Form** – real-time dan on-submit.
- **Interaktivitas** – animasi, efek sentuh, transisi halus.

---

## Teknologi yang Digunakan

| Teknologi           | Keterangan                                        |
| ------------------- | ------------------------------------------------- |
| HTML5               | Struktur halaman                                  |
| CSS3                | Gaya dengan Tailwind CSS (via CDN)                |
| Tailwind CSS        | Framework utility-first untuk styling             |
| Vanilla JavaScript  | Logika aplikasi, DOM manipulation, event handling |
| localStorage        | Penyimpanan data transaksi di sisi klien          |
| QRCode.js (CDN)     | Menghasilkan QR code untuk metode QRIS            |
| Font Google (Inter) | Tipografi utama                                   |
| Material Symbols    | Ikon dari Google                                  |

---

## Cara Menjalankan

1. **Unduh** atau **clone** repositori ini.
2. Pastikan Anda memiliki koneksi internet (untuk mengakses CDN).
3. Buka file **`index.html`** di browser (disarankan Google Chrome atau Firefox).
4. Aplikasi siap digunakan. Semua data dummy sudah tersedia di dalam kode JavaScript.

> **Catatan:** Tidak perlu server atau instalasi tambahan. Semua berjalan di sisi klien.

---

## Struktur Data Dummy

Data tagihan dan SPP disimpan dalam objek `BILL_DATA` di JavaScript. Contoh:

```javascript
const BILL_DATA = {
  pln: {
    123456789012: {
      name: "Budi Santoso",
      address: "Jl. Merdeka No. 123, Jakarta",
      period: "Jan-Feb 2025",
      amount: 245000,
      fine: 0,
      dueDate: "2025-02-15",
    },
  },
  spp: {
    202310001: [
      {
        id: 1,
        desc: "SPP Semester Ganjil 2025/2026 - Cicilan ke-1",
        amount: 2500000,
        status: "unpaid",
      },
      // ...
    ],
  },
};
```
