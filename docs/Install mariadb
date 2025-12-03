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
