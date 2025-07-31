# CPI Tagging App

Aplikasi web sederhana berbasis Flask untuk memproses gambar dengan menambahkan ID, tanggal/waktu, dan informasi OCR (Optical Character Recognition) yang diekstraksi. Gambar yang telah diproses kemudian dapat diunduh secara otomatis.

## Daftar Isi

* [Fitur](#fitur)
* [Tumpukan Teknologi](#tumpukan-teknologi)
* [Struktur Proyek](#struktur-proyek)
* [Persyaratan Font](#persyaratan-font)
* [Pengaturan & Jalankan Secara Lokal](#pengaturan--jalankan-secara-lokal)
* [Deployment di Ubuntu 20.04](#deployment-di-ubuntu-2004)
* [Batasan Diketahui & Peningkatan di Masa Depan](#batasan-diketahui--peningkatan-di-masa-depan)
* [Lisensi](#lisensi)

---

## Fitur

* **Unggah Gambar Fleksibel**: Mendukung unggah gambar melalui:
    * Klik tombol "Browse".
    * Seret dan lepas (Drag & Drop) ke seluruh halaman web.
    * Tempel (Paste) gambar langsung dari clipboard.
* **Input ID Otomatis/Manual**:
    * Mendukung tempel (paste) teks ID langsung ke halaman web (akan otomatis mengisi kolom ID).
    * Memformat ID secara otomatis ke huruf kapital dan menghilangkan spasi (baik di frontend maupun backend).
    * Fokus otomatis ke kolom ID dan hapus satu karakter saat `Backspace` ditekan di luar input.
    * Reset formulir dengan menekan `Esc`.
* **Pratinjau Gambar**: Menampilkan pratinjau gambar asli yang diunggah di sisi kanan layar.
* **Penambahan Metadata ke Gambar**:
    * Menambahkan ID yang dimasukkan.
    * Menambahkan tanggal dan waktu saat ini (WIB) ke gambar.
    * Menambahkan nilai C/N dan CPI yang diekstraksi melalui OCR (Optical Character Recognition) dari area tertentu pada gambar.
* **Kustomisasi Teks**:
    * Teks ID ditampilkan dengan gaya **bold**.
    * Teks C/N dan CPI ditampilkan dengan gaya *italic*.
* **Transparansi Logo**: Logo yang ditimpa memiliki tingkat transparansi yang dapat dikonfigurasi.
* **Nama File Unduhan Otomatis**: Hasil gambar diunduh dengan nama file yang diformat sebagai `ID_DD Bulan YYYY.png`.
* **Pengukuran Waktu Proses**: Menampilkan waktu yang dibutuhkan untuk memproses gambar (termasuk upload, pemrosesan server, dan download).

## Tumpukan Teknologi

* **Backend**: Python, Flask, Gunicorn
* **Manipulasi Gambar**: Pillow (PIL)
* **OCR**: Pytesseract (dengan mesin Tesseract OCR)
* **Deployment**: Nginx
* **Frontend**: HTML5, CSS3, JavaScript
* **Pengelolaan Dependensi**: `pip`, `venv`

## Struktur Proyek

cpi-tagging-app/
├── app.py                  # Aplikasi Flask utama (backend)
├── requirements.txt        # Daftar dependensi Python
├── static/                 # File statis (CSS, gambar logo, font)
│   ├── style.css           # Styling CSS
│   ├── logo_psn.png        # File logo
│   ├── ARIAL.TTF           # Font Arial Reguler
│   ├── ARIALBD.TTF         # Font Arial Bold
│   └── ARIALIT.TTF         # Font Arial Italic
└── templates/              # Template HTML
└── index.html          # Halaman utama aplikasi
