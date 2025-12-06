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

Tampilkan konfigurasi antarmuka jaringan, kemudian catat inet alamat IP dari virtual machine debian 12 pada bagian yang bertanda xxx
```
ifconfig
```

ens33: flags=4163  mtu 1500
        inet xxx.xxx.xxx.xxx  netmask 255.255.255.0  broadcast 192.168.83.255
        inet6 fe80::20c:29ff:fe4b:9846  prefixlen 64  scopeid 0x20
        ether 00:0c:29:4b:98:46  txqueuelen 1000  (Ethernet)
        RX packets 183076  bytes 261621540 (249.5 MiB)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 49109  bytes 3753808 (3.5 MiB)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0


    Tambahkan entri host pada sistem operasi windows agar hostname repositori yang terinstal di Debian (Virtual Machine) dapat diakses di browser windows.
1.Buka Notepad sebagai Administrator:
  • Klik kanan pada ikon Notepad atau perangkat lunak teks editor lainnya.
  • Pilih "Run as administrator."
2.Buka File Hosts:
  • Di jendela Notepad, klik menu "File" > "Open"
  • Navigasi ke direktori C:\Windows\System32\drivers\etc\
  • Pilih opsi "All Files" di bagian bawah jendela.
  • Pilih file hosts dan klik "Open".
3.Tambahkan Entri Baru:
  • Di bagian akhir file hosts, tambahkan baris baru yang menjelaskan ip address dan hostname repositori.
  • Formatnya adalah <alamat_IP> <space> <nama_domain> contoh: 192.168.253.153 repositori.tes.ac.id
4.Simpan perubahan dengan menekan Ctrl + S

Buka Browser (Chrome, Firefox, Edge, Opera dll.) dan coba akses hostname repositori pada address bar
```
repositori.tes.ac.id
```
