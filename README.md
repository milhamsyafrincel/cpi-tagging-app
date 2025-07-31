# CPI Tagging App

Aplikasi Web simple berbasis Flask untuk memberikan Tag pada hasil screenshot (image) pengecekan carrier dari Decimator. Tag yang diberikan berupa logo, ID, Tanggal/Jam (WIB), dan nilai C/N & CPI yang di extract dari screenshoot tersebut. Screenshot yang sudah diproses akan terdownload secara otomatis.

## Daftar Isi

* [Fitur](#fitur)
* [Technology Stack](#technology-stack)
* [Project Structure](#project-structure)
* [Persyaratan Font](#persyaratan-font)
* [Pengaturan & Jalankan Secara Lokal](#pengaturan--jalankan-secara-lokal)
* [Deployment di Ubuntu 20.04](#deployment-di-ubuntu-2004)
* [Batasan Diketahui & Peningkatan di Masa Depan](#batasan-diketahui--peningkatan-di-masa-depan)
* [Lisensi](#lisensi)

---

## Fitur

* **Input ID Otomatis/Manual**:
    * Paste teks ID langsung ke halaman web (akan otomatis mengisi kolom ID).
    * Memformat ID secara otomatis ke huruf kapital dan menghilangkan spasi.
    * Tekan tombol `Backspace` dimanapun akan menghapus 1 karakter pada kolom ID.
* **Upload Image Fleksibel**: Mendukung upload melalui:
    * Klik tombol "Browse".
    * Drag & Drop pada seluruh halaman web.
    * Paste langsung dari clipboard.
* **Preview Image**: Menampilkan image yang di upload di sisi kanan layar.
* **Delete Image Mudah**:Tekan tombol `Esc` dimanapun akan menghapus image yang sudah di-upload.
* **Penambahan Metadata ke Gambar**:
    * Menambahkan ID yang dimasukkan.
    * Menambahkan tanggal dan waktu saat ini (WIB) ke gambar.
    * Menambahkan nilai C/N dan CPI yang diekstraksi melalui OCR (Optical Character Recognition) dari area tertentu pada gambar.
* **Rename File Otomatis**: Download hasil image dengan nama file yang diformat sebagai `ID_DD Bulan YYYY.png`

## Technology Stack

* **Backend**: Python, Flask, Gunicorn
* **Image Processing**: Pillow (PIL)
* **OCR**: Pytesseract (with OCR Tesseract machine)
* **Deployment**: Nginx
* **Frontend**: HTML5, CSS3, JavaScript
* **Dependency Management**: `pip`, `venv`

## Project Structure
```
cpi-tagging-app/
├── app.py                     
├── requirements.txt           
├── static/                    
│   ├── style.css              
│   ├── logo_psn.png           
│   ├── ARIAL.TTF              
│   ├── ARIALBD.TTF            
│   └── ARIALIT.TTF            
└── templates/                 
    └── index.html             
```
