# CPI Tagging App

Aplikasi Web simple berbasis Flask untuk memberikan Tag pada hasil screenshot (image) pengecekan carrier dari Decimator. Tag yang diberikan berupa logo, ID, Tanggal/Jam (WIB), dan nilai C/N & CPI yang di extract dari screenshoot tersebut. Screenshot yang sudah diproses akan terdownload secara otomatis.

## Daftar Isi

* [Fitur](#fitur)
* [Technology Stack](#technology-stack)
* [Project Structure](#project-structure)
* [Step Guidance](#step-guidance)
* [Batasan](#batasan)

---

## Fitur

* **Input ID Otomatis/Manual**:
    * Paste ID langsung dimanapun pada halaman web (akan otomatis mengisi kolom ID).
    * Memformat ID secara otomatis ke huruf kapital dan menghilangkan spasi.
    * Tekan tombol `Backspace` dimanapun akan menghapus 1 karakter pada kolom ID.
* **Upload Image Fleksibel**: Mendukung upload melalui:
    * Klik tombol "Browse".
    * Drag & Drop dimanapun pada seluruh halaman web.
    * Paste langsung dari clipboard.
* **Preview Image**: Menampilkan image yang di upload di sisi kanan layar.
* **Delete Image Mudah**:Tekan tombol `Esc` dimanapun akan menghapus image yang sudah di-upload.
* **Penambahan Metadata ke Image**:
    * Menambahkan ID yang dimasukkan.
    * Menambahkan tanggal dan waktu saat ini (WIB) ke image.
    * Menambahkan nilai C/N dan CPI yang diekstraksi melalui OCR (Optical Character Recognition) dari area tertentu pada image.
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

## Step Guidance

Ikuti langkah-langkah berikut untuk menjalankan aplikasi di komputer lokal (untuk pengembangan dan pengujian).

1.  **Update Sistem**
    ```bash
    sudo apt update
    sudo apt upgrade -y
    ```
2. **Install Python, pip, dan virtualenv**
    ```bash
    sudo apt install python3-pip python3-venv -y
    ```
3. **Install Tesseract OCR (OCR Machine, not Python Library)**
    ```
    sudo apt install tesseract-ocr -y
    ```
4. **Install Git**
   ```bash
   sudo apt install git -y
   ```
5. **Install Nginx:**
    ```bash
    sudo apt install nginx -y
    ```
6. **Install Gunicorn: WSGI server untuk running aplikasi Flask**
    ```bash
    pip install gunicorn
    ```
7. **Buat file directory**
    ```bash
    sudo mkdir -p /var/www/cpi_tagging_app
    sudo chown -R $USER:$USER /var/www/cpi_tagging_app
    cd /var/www/cpi_tagging_app
    ```
8. **Clone Project** 
    ```bash
    git clone [https://github.com/milhamsyafrincel/cpi-tagging-app.git]
    ```
9. **Buat dan Aktifkan Virtual Environment:**
    ```bash
    python3 -m venv venv
    source venv/bin/activate
    ```
10. **Install Python Dependecies**
    ```bash
    pip install -r requirements.txt
    ```
11. **Konfigurasi Gunicorn**
    Buat service `systemd`
    ```bash
    sudo nano /etc/systemd/system/cpi_tagging_app.service
    ```

    Isi dengan content berikut
    ```
    [Unit]
    Description=Gunicorn instance to serve CPI Tagging App
    After=network.target

    [Service]
    User=your_username
    Group=www-data                
    WorkingDirectory=/var/www/cpi_tagging_app
    ExecStart=/var/www/cpi_tagging_app/venv/bin/gunicorn --workers 3 --bind unix:/var/www/cpi_tagging_app/cpi_tagging_app.sock -m 007 app:app
    Restart=always
    StandardOutput=syslog
    StandardError=syslog

    [Install]
    WantedBy=multi-user.target
    ```

    Note: Isi `your_username` dengan username computer

    Reload, aktifkan, dan start service `systemd`
    ```bash
    sudo systemctl daemon-reload
    sudo systemctl start cpi_tagging_app
    sudo systemctl enable cpi_tagging_app
    ```

12. **Konfigurasi Nginx (Reverse Proxy)**
    Buat file konfigurasi Nginx
    ```bash
    sudo nano /etc/nginx/sites-available/cpi_tagging_app
    ```

    Isi dengan content berikut
    ```
    server {
       listen 80;
       
       location / {
           include proxy_params;
           proxy_pass http://unix:/var/www/cpi_tagging_app/cpi_tagging_app.sock;
           proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
           proxy_set_header X-Forwarded-Proto $scheme;
           proxy_set_header Host $http_host;
           proxy_redirect off;

           # Pengaturan timeout untuk proses yang lama
           proxy_connect_timeout 600s;
           proxy_send_timeout 600s;
           proxy_read_timeout 600s;
           send_timeout 600s;
       }

       location /static {
           alias /var/www/cpi_tagging_app/static; # Serve file statis langsung dari Nginx
       }
    }
    ```

    Aktifkan Nginx
    ```bash
    sudo ln -s /etc/nginx/sites-available/cpi_tagging_app /etc/nginx/sites-enabled
    ```

    Uji Confgi Nginx dan restart
    ```bash
    sudo nginx -t
    sudo systemctl restart nginx
    ```
13. **Konfigurasi Firewall (UFW)**
    Izinkan traffic HTTP
    ```bash
    sudo ufw allow 'Nginx HTTP'
    sudo ufw enable # Aktifkan UFW jika belum aktif
    ```
 
## Batasan 

* **Kinerja OCR**: Saat ini, OCR menggunakan Region of Interest (ROI) tetap, yang mungkin tidak konsisten pada semua gambar.
