# PSAT2425

Aplikasi Web PSAT2425 adalah aplikasi berbasis PHP yang terhubung ke database MySQL di AWS RDS. Aplikasi ini dapat dideploy otomatis menggunakan EC2 User Data.

## 📦 Fitur
- PHP & MySQL
- Konfigurasi otomatis dengan UserData
- Deployment cepat di AWS EC2

---

## 🚀 Langkah Deploy di AWS

### 1. Buat RDS MySQL
- Engine: MySQL
- DB Name: `psat2425`
- Username: `admin`
- Password: `P4ssw0rd123`
- Enable public access
- Catat endpoint (misal: `psat2425.ck0pitmttnal.us-east-1.rds.amazonaws.com`)

### 2. Launch EC2 Instance
- Nama terserah
- OS: Ubuntu
- Instance Type: t2.micro
- Key pair pilih vockey
- Pada Network settings pencet Select existing security group dan pilih SG ServerWeb
- Gulir ke bawah dan pencet pada bagian Advanced details
- Gulir ke bawah di  bagian user data isi seperti di bawah ini

### 3. Masukkan User Data saat Launch:

```bash
#!/bin/bash
sudo apt update -y
sudo apt install -y apache2 php php-mysql libapache2-mod-php mysql-client
sudo rm -rf /var/www/html/{*,.*}
sudo git clone https://github.com/<GITHUBMU>/psat2425.git /var/www/html
sudo chmod -R 777 /var/www/html
echo DB_USER=admin > /var/www/html/.env
echo DB_PASS=P4ssw0rd123 >> /var/www/html/.env
echo DB_NAME=psat2425 >> /var/www/html/.env
echo DB_HOST=psat2425.ck0pitmttnal.us-east-1.rds.amazonaws.com >> /var/www/html/.env
