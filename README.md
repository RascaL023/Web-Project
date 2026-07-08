
<p align="center">
  <img src="Public/assets/hero.jpg" alt="WarAs Banner" width="100%">
</p>

<h1 align="center">WarAs (Warehouse Aswan)</h1>

<p align="center">
  <strong>Aplikasi manajemen inventori dan transaksi harian untuk UMKM dan usaha rumahan.</strong>
  <br>
  Mudah, ringan, dan fleksibel — cukup jalankan di browser.
</p>

<p align="center">
  <img src="https://img.shields.io/badge/status-active-brightgreen" alt="Status">
  <img src="https://img.shields.io/badge/stack-vanilla%20JS%20%7C%20Firebase-blue" alt="Stack">
  <img src="https://img.shields.io/badge/license-MIT-lightgrey" alt="License">
</p>

---

## Daftar Isi

- [Fitur](#fitur)
- [Tech Stack](#tech-stack)
- [Struktur Proyek](#struktur-proyek)
- [Prasyarat](#prasyarat)
- [Menjalankan Aplikasi](#menjalankan-aplikasi)
- [Kompilasi SCSS](#kompilasi-scss)
- [Struktur Database Firebase](#struktur-database-firebase)
- [Konfigurasi](#konfigurasi)
- [Tampilan](#tampilan)
- [Kontribusi](#kontribusi)
- [Lisensi](#lisensi)

---

## Fitur

| Fitur | Deskripsi |
|---|---|
| **Registrasi & Login** | Daftar akun baru atau masuk dengan email & password. Data tersimpan di Firebase. |
| **Dashboard** | Ringkasan pendapatan kotor, total barang, stok aktif, transaksi hari ini, pemasukan & pengeluaran. |
| **Manajemen Inventori** | Lihat daftar barang lengkap dengan stok, satuan, dan tanggal update. Dilengkapi pencarian. |
| **Transaksi** | Catat barang masuk atau keluar. Total harga otomatis dihitung. Stok diperbarui otomatis. |
| **Histori Transaksi** | Riwayat transaksi dengan filter tanggal dan jenis (semua / masuk / keluar). |
| **Tema Gelap/Terang** | Beralih antara mode terang dan gelap. Preferensi tersimpan di `localStorage`. |
| **Responsive Design** | Tampilan mobile-friendly dengan navigasi hamburger dan grid responsif. |

---

## Tech Stack

| Lapisan | Teknologi |
|---|---|
| **Frontend** | HTML5, CSS3, JavaScript (ES6+) — vanilla, tanpa framework |
| **Styling** | SCSS (dikompilasi ke CSS via Dart Sass) |
| **Ikon** | Google Material Symbols Rounded |
| **Font** | Montserrat, Michroma, Yellowtail (Google Fonts) |
| **Database** | Firebase Realtime Database (via REST API) |
| **Auth** | `localStorage` + validasi session ke Firebase |

---

## Struktur Proyek

```
WarAs/
├── index.html                    # Halaman utama (landing page)
├── .gitignore
├── .vscode/
│   └── settings.json             # Konfigurasi Live Server (port 8888)
└── Public/
    ├── assets/
    │   ├── Hamburger.svg         # Ikon menu mobile
    │   ├── hero.jpg              # Gambar hero section
    │   └── Setting.svg           # Ikon pengaturan
    ├── css/
    │   ├── style.css             # CSS hasil kompilasi
    │   └── style.css.map         # Sourcemap
    ├── js/
    │   └── script.js             # Logika utama aplikasi
    ├── pages/
    │   ├── dashboard.html        # Halaman dashboard
    │   ├── histori.html          # Histori transaksi
    │   ├── inventori.html        # Manajemen inventori
    │   ├── log-reg.html          # Halaman login & registrasi
    │   └── transaksi.html        # Form transaksi
    └── scss/
        ├── _color.scss           # Variabel tema, mixin, animasi
        └── style.scss            # Stylesheet utama SCSS
```

---

## Prasyarat

Tidak ada dependensi khusus. Cukup:

- Browser modern (Chrome, Firefox, Edge, Safari)
- *(Opsional)* VS Code + ekstensi [Live Server](https://marketplace.visualstudio.com/items?itemName=ritwickdey.LiveServer)
- *(Opsional)* Dart Sass — jika ingin mengompilasi ulang SCSS:
  ```bash
  npm install -g sass
  ```

---

## Menjalankan Aplikasi

### Opsi A — VS Code Live Server (Direkomendasikan)

```bash
code .
# Klik kanan index.html > "Open with Live Server"
# Aplikasi berjalan di http://127.0.0.1:8888
```

### Opsi B — Python HTTP Server

```bash
python3 -m http.server 8080
```

### Opsi C — npx serve

```bash
npx serve .
```

> **Catatan:** Membuka `index.html` langsung dari file system dapat menyebabkan masalah CORS pada request ke Firebase. Gunakan Live Server atau HTTP server.

---

## Kompilasi SCSS

Jika Anda mengubah file `.scss`, kompilasi ulang ke CSS:

```bash
sass Public/scss/style.scss Public/css/style.css
```

Gunakan flag `--watch` untuk kompilasi otomatis:

```bash
sass --watch Public/scss/style.scss Public/css/style.css
```

---

## Struktur Database Firebase

Aplikasi ini menggunakan **Firebase Realtime Database** dengan struktur berikut:

```json
{
  "users_meta": {
    "<uid>": {
      "nama": "Nama Pengguna",
      "email": "user@example.com",
      "password": "userpassword",
      "theme": "l"
    }
  },
  "users_data": {
    "<uid>": {
      "barang": {
        "<itemId>": {
          "a_namaBarang": "Nama Barang",
          "b_stok": 10,
          "c_satuan": "pcs",
          "d_tanggal": "2025-01-15"
        }
      }
    }
  },
  "transaksi": {
    "<uid>": {
      "pemasukan": { "...": { ... } },
      "pengeluaran": { "...": { ... } }
    }
  },
  "histori": {
    "<uid>": {
      "<hisId>": {
        "a_idBarang": "...",
        "aa_idTransaksi": "...",
        "b_tanggal": "...",
        "c_jenis": "pemasukan",
        "d_nominal": 50000,
        "e_deskripsi": "..."
      }
    }
  }
}
```

---

## Konfigurasi

### Mengganti Database Firebase

Ubah konstanta `root` di `Public/js/script.js:1`:

```js
const root = 'https://warasapi-default-rtdb.asia-southeast1.firebasedatabase.app';
```

### Port Live Server

Ubah port di `.vscode/settings.json`:

```json
{
  "liveServer.settings.port": 8888
}
```

---

## Tampilan

| Halaman | Deskripsi |
|---|---|
| **Landing Page** | Hero section, fitur unggulan, CTA menuju login |
| **Login / Register** | Form registrasi & login dengan animasi slide |
| **Dashboard** | Kartu ringkasan + daftar barang + transaksi hari ini |
| **Inventori** | Tabel barang dengan pencarian real-time |
| **Transaksi** | Form input barang masuk/keluar |
| **Histori** | Riwayat transaksi dengan filter tanggal & jenis |

---

## Kontribusi

Kontribusi selalu terbuka! Silakan buka *issue* atau kirim *pull request*.

1. *Fork* repositori ini
2. Buat branch fitur Anda (`git checkout -b fitur-keren`)
3. *Commit* perubahan (`git commit -m 'feat: tambah fitur keren'`)
4. *Push* ke branch (`git push origin fitur-keren`)
5. Buka *Pull Request*

---

## Lisensi

Proyek ini dilisensikan di bawah **MIT License** — lihat file [LICENSE](LICENSE) untuk detail lebih lanjut.

---

<p align="center">
  Made with ❤️ for UMKM Indonesia
  <br>
  © 2025 WarAs
</p>
