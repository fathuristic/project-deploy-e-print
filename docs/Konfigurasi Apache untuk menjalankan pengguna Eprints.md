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
