Install dependencies eprints

```
  sudo apt install perl libncurses5 apache2 libapache2-mod-perl2 \
libxml-libxml-perl libunicode-string-perl libterm-readkey-perl \
libmime-lite-perl libmime-types-perl libdigest-sha-perl libdbd-mysql-perl \
libxml-parser-perl libxml2-dev libxml-twig-perl libarchive-any-perl \
libjson-perl liblwp-protocol-https-perl libtext-unidecode-perl lynx wget \
ghostscript poppler-utils antiword elinks texlive-base texlive-binaries \
psutils imagemagick adduser tar gzip unzip libsearch-xapian-perl \
libtex-encode-perl libio-string-perl python3-html2text make \
libexpat1-dev libxslt1-dev git
```

Install mariadb

```
sudo apt-get install apt-transport-https curl
sudo mkdir -p /etc/apt/keyrings
sudo curl -o /etc/apt/keyrings/mariadb-keyring.pgp 'https://mariadb.org/mariadb_release_signing_key.pgp'
```
masukkan folder
```
sudo nano /etc/apt/sources.list.d/mariadb.sources
```
```
# MariaDB 12.1 repository list - created 2025-12-02 10:17 UTC
# https://mariadb.org/download/
X-Repolib-Name: MariaDB
Types: deb
# deb.mariadb.org is a dynamic mirror if your preferred mirror goes offline. See https://mariadb.org/mirrorbits/ for details.
# URIs: https://deb.mariadb.org/12.1/debian
URIs: https://mr.heru.id/mariadb/repo/12.1/debian
Suites: debian
Components: main
Signed-By: /etc/apt/keyrings/mariadb-keyring.pgp
```
update dan install
```
sudo apt-get update
sudo apt-get install mariadb-server
```


buat user baru
```
sudo adduser eprints
```

Buka file envvars dengan teks editor nano dengan perintah berikut:
```
nano /etc/apache2/envvars
```
Salin dan tambahkan baris berikut:

```
export APACHE_RUN_USER=eprints
export APACHE_RUN_GROUP=eprints
```

Download file source EPrints dan repositori variasi publikasi

```
wget https://files.eprints.org/3288/1/eprints-3.4.7.tar.gz https://files.eprints.org/3288/2/eprints-3.4.7-flavours.tar.gz
```

Ekstrak file tar source EPrints dan repositori variasi publikasi
```
tar xvzf eprints-3.4.7.tar.gz && tar xvzf eprints-3.4.7-flavours.tar.gz
```

Pindah ke folder source EPrints
```
cd eprints-3.4.7
```

Jalankan perintah di bawah untuk konfigurasi EPrints
```
./configure
```

Instalasi Eprints berdasarkan kompilasi dependensi
```
make install
```

Beralih ke pengguna EPrints
```
su - eprints
```

Pindah ke folder EPrints
```
cd /opt/eprints3
```

Jalankan aplikasi epadmin untuk membuat repositori beserta setting Eprints
```
bin/epadmin create pub
```

Keluar dari pengguna EPrints
```
exit
```

Buat file configurasi eprints.conf di apache dengan menggunakan teks editor nano dengan menjalankan perintah di bawah ini:
```
nano /etc/apache2/sites-available/eprints.conf
```

```
Include /opt/eprints3/cfg/apache.conf
```

Aktifkan konfigurasi virtual host dari aplikasi EPrints
```
a2ensite eprints
```

Muat ulang konfigurasi apache
```
systemctl reload apache2
```

Non-aktifkan situs web default apache
```
a2dissite 000-default
```

Muat ulang konfigurasi apache
```
systemctl reload apache2
```

Restart service apache
```
service apache2 restart
```

Install aplikasi net-tools untuk mengetahui informasi jaringan dari virtual machine
```
apt install net-tools
```

Tampilkan konfigurasi antarmuka jaringan, kemudian catat inet alamat IP dari virtual machine debian 12
```
ip a
```
<img width="840" height="293" alt="image" src="https://github.com/user-attachments/assets/d66301dc-6b6a-453b-bc3b-9988b7681634" />




Buka Browser (Chrome, Firefox, Edge, Opera dll.) dan coba akses hostname repositori pada address bar
```
127.0.0.1
```

