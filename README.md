# CPI Tagging App

Aplikasi Web simple berbasis Flask untuk memberikan Tag pada hasil screenshot pengecekan carrier via Decimator. Tag yang diberikan berupa logo PSN, ID, Tanggal/Jam (WIB), dan nilai C/N & CPI yang di extract dari screenshoot tersebut. Screenshot yang sudah diproses akan terdownload secara otomatis.

## Daftar Isi

* [Fitur](#fitur)
* [Technology Stack](#technology-stack)
* [Struktur Proyek](#struktur-proyek)
* [Persyaratan Font](#persyaratan-font)
* [Pengaturan & Jalankan Secara Lokal](#pengaturan--jalankan-secara-lokal)
* [Deployment di Ubuntu 20.04](#deployment-di-ubuntu-2004)
* [Batasan Diketahui & Peningkatan di Masa Depan](#batasan-diketahui--peningkatan-di-masa-depan)
* [Lisensi](#lisensi)

---

## Fitur

* **Upload Screenshoot Fleksibel**: Mendukung upload melalui:
    * Klik tombol "Browse".
    * Drag & Drop pada seluruh halaman web.
    * Paste langsung dari clipboard.
* **Input ID Otomatis/Manual**:
    * Paste teks ID langsung ke halaman web (akan otomatis mengisi kolom ID).
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

## Technology Stack

* **Backend**: Python, Flask, Gunicorn
* **Image Processing**: Pillow (PIL)
* **OCR**: Pytesseract (with OCR Tesseract machine)
* **Deployment**: Nginx
* **Frontend**: HTML5, CSS3, JavaScript
* **Dependency Management**: `pip`, `venv`

## Struktur Proyek

cpi-tagging-app/ \n
├── app.py                  # Aplikasi Flask utama (backend) /n
├── requirements.txt        # Daftar dependensi Python
├── static/                 # File statis (CSS, gambar logo, font)
│   ├── style.css           # Styling CSS
│   ├── logo_psn.png        # File logo
│   ├── ARIAL.TTF           # Font Arial Reguler
│   ├── ARIALBD.TTF         # Font Arial Bold
│   └── ARIALIT.TTF         # Font Arial Italic
└── templates/              # Template HTML
└── index.html          # Halaman utama aplikasi
