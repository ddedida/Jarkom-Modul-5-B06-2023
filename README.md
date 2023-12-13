# Jarkom-Modul-5-B06-2023

**Laporan Resmi Praktikum Jaringan Komputer Modul 5**

| Nama                   | NRP        |
| ---------------------- | ---------- |
| M. Dafian Zaki Akhdan  | 5025211108 |
| Dewangga Dika Darmawan | 5025211109 |

## Soal Nomor 0

Setelah pandai mengatur jalur-jalur khusus, kalian diminta untuk membantu North Area menjaga wilayah mereka dan kalian dengan senang hati membantunya karena ini merupakan tugas terakhir.

#### Tugas pertama, buatlah peta wilayah sesuai berikut ini:

![image](https://github.com/ddedida/Jarkom-Modul-5-B06-2023/assets/108203648/a77e6d89-a0ba-41b0-bf5f-5666f11ee571)

**Keterangan:**

```
Richter adalah DNS Server
Revolte adalah DHCP Server
Sein dan Stark adalah Web Server
Jumlah Host pada SchwerMountain adalah 64
Jumlah Host pada LaubHills adalah 255
Jumlah Host pada TurkRegion adalah 1022
Jumlah Host pada GrobeForest adalah 512
```

#### Untuk menghitung rute-rute yang diperlukan, gunakan perhitungan dengan metode VLSM. Buat juga pohonnya, dan lingkari subnet yang dilewati:

-   **Pembagian rute:**

![bjir1](https://github.com/ddedida/Jarkom-Modul-5-B06-2023/assets/108203648/4a17f030-eda4-4199-ad57-dd583fdc3269)

![image](https://github.com/ddedida/Jarkom-Modul-5-B06-2023/assets/108203648/7968bc9a-c2cb-40db-bbac-f9a8ee659fde)

-   **Tree VLSM:**

<img width="1826" alt="bjir" src="https://github.com/ddedida/Jarkom-Modul-5-B06-2023/assets/108203648/7b3100e5-bad2-4dce-9ebc-2ca9b27aaaa0">

#### Kemudian buatlah rute sesuai dengan pembagian IP yang kalian lakukan:

![image](https://github.com/ddedida/Jarkom-Modul-5-B06-2023/assets/108203648/b72f7902-a130-4586-adfc-7dcf80626252)

Berikut merupakan [link](<[https://github.com/user/repo/blob/branch/other_file.md](https://docs.google.com/spreadsheets/d/18h_e6yaBEORnPLRlbLNUG6ELZ2ZwMwkHk0R6c12TuhY/edit?usp=sharing)https://docs.google.com/spreadsheets/d/18h_e6yaBEORnPLRlbLNUG6ELZ2ZwMwkHk0R6c12TuhY/edit?usp=sharing>) spreadsheet untuk pembagian ip masing-masing node.

**Konfigurasi Subnetting (setiap node) dan Routing (Aura, Frieren, dan Himmel):**

-   Aura

```sh
# Static config for eth0
auto eth0
iface eth0 inet dhcp

# Static config for eth1
auto eth1
iface eth1 inet static
	address 192.181.15.105
	netmask 255.255.255.252

# Static config for eth2
auto eth2
iface eth2 inet static
	address 192.181.15.109
	netmask 255.255.255.252

# Routing eth1
up route add -net 192.181.0.0 netmask 255.255.248.0 gw 192.181.15.106
up route add -net 192.181.8.0 netmask 255.255.252.0 gw 192.181.15.106

# Routing eth2
up route add -net 192.181.15.112 netmask 255.255.255.252 gw 192.181.15.110
up route add -net 192.181.15.116 netmask 255.255.255.252 gw 192.181.15.110
up route add -net 192.181.12.0 netmask 255.255.254.0 gw 192.181.15.110
up route add -net 192.181.15.128 netmask 255.255.255.128 gw 192.181.15.110
up route add -net 192.181.15.120 netmask 255.255.255.252 gw 192.181.15.110
up route add -net 192.181.15.124 netmask 255.255.255.252 gw 192.181.15.110
```

-   Heiter

```sh
# Static config for eth0
auto eth0
iface eth0 inet static
	address 192.181.15.106
	netmask 255.255.255.252
	gateway 192.181.15.105

# Static config for eth1
auto eth1
iface eth1 inet static
	address 192.181.0.1
	netmask 255.255.248.0

# Static config for eth2
auto eth2
iface eth2 inet static
	address 192.181.8.1
	netmask 255.255.252.0

up echo nameserver 192.168.122.1 > /etc/resolv.conf
```

-   TurkRegion (1022 Host)

```sh
# Static config for eth0
auto eth0
iface eth0 inet dhcp
	gateway 192.181.0.1

up echo nameserver 192.168.122.1 > /etc/resolv.conf
```

-   Sein (Web Server)

```sh
# Static config for eth0
auto eth0
iface eth0 inet static
	address 192.181.8.2
	netmask 255.255.252.0
	gateway 192.181.8.1

up echo nameserver 192.168.122.1 > /etc/resolv.conf
```

-   GrobeForest (512 Host)

```sh
# Static config for eth0
auto eth0
iface eth0 inet dhcp
        gateway 192.181.8.1

up echo nameserver 192.168.122.1 > /etc/resolv.conf
```

-   Frieren

```sh
# Static config for eth0
auto eth0
iface eth0 inet static
	address 192.181.15.110
	netmask 255.255.255.252
	gateway 192.181.15.109

# Static config for eth1
auto eth1
iface eth1 inet static
	address 192.181.15.113
	netmask 255.255.255.252

# Static config for eth2
auto eth2
iface eth2 inet static
	address 192.181.15.117
	netmask 255.255.255.252

up echo nameserver 192.168.122.1 > /etc/resolv.conf

# Routing eth2
up route add -net 192.181.12.0 netmask 255.255.254.0 gw 192.181.15.118
up route add -net 192.181.15.128 netmask 255.255.255.128 gw 192.181.15.118
up route add -net 192.181.15.120 netmask 255.255.255.252 gw 192.181.15.118
up route add -net 192.181.15.124 netmask 255.255.255.252 gw 192.181.15.118
```

-   Stark (Web Server)

```sh
# Static config for eth0
auto eth0
iface eth0 inet static
	address 192.181.15.114
	netmask 255.255.255.252
	gateway 192.181.15.113

up echo nameserver 192.168.122.1 > /etc/resolv.conf
```

-   Himmel

```sh
# Static config for eth0
auto eth0
iface eth0 inet static
	address 192.181.15.118
	netmask 255.255.255.252
	gateway 192.181.15.117

# Static config for eth1
auto eth1
iface eth1 inet static
	address 192.181.12.1
	netmask 255.255.254.0

# Static config for eth2
auto eth2
iface eth2 inet static
	address 192.181.15.129
	netmask 255.255.255.128

up echo nameserver 192.168.122.1 > /etc/resolv.conf

# Routing eth2
up route add -net 192.181.15.120 netmask 255.255.255.252 gw 192.181.15.130
up route add -net 192.181.15.124 netmask 255.255.255.252 gw 192.181.15.130
```

-   LaubHills (255 Host)

```sh
# Static config for eth0
auto eth0
iface eth0 inet dhcp
	gateway 192.181.12.1

up echo nameserver 192.168.122.1 > /etc/resolv.conf
```

-   SchwerMountain (64 Host)

```sh
# Static config for eth0
auto eth0
iface eth0 inet dhcp
	gateway 192.181.15.129

up echo nameserver 192.168.122.1 > /etc/resolv.conf
```

-   Fern

```sh
# Static config for eth0
auto eth0
iface eth0 inet static
	address 192.181.15.130
	netmask 255.255.255.128
	gateway 192.181.15.129

# Static config for eth1
auto eth1
iface eth1 inet static
	address 192.181.15.121
	netmask 255.255.255.252

# Static config for eth2
auto eth2
iface eth2 inet static
	address 192.181.15.125
	netmask 255.255.255.252

up echo nameserver 192.168.122.1 > /etc/resolv.conf
```

-   Ritcher (DNS Server)

```sh
# Static config for eth0
auto eth0
iface eth0 inet static
	address 192.181.15.122
	netmask 255.255.255.252
	gateway 192.181.15.121

up echo nameserver 192.168.122.1 > /etc/resolv.conf
```

-   Revolte (DHCP Server)

```sh
# Static config for eth0
auto eth0
iface eth0 inet static
	address 192.181.15.126
	netmask 255.255.255.252
	gateway 192.181.15.125

up echo nameserver 192.168.122.1 > /etc/resolv.conf
```

#### Tugas berikutnya adalah memberikan ip pada subnet SchwerMountain, LaubHills, TurkRegion, dan GrobeForest menggunakan bantuan DHCP:

**Revolte (DHCP Server)**

-   dhcp.conf

```sh
# A1
subnet 192.181.15.104 netmask 255.255.255.252 {
}

# A2
subnet 192.181.0.0 netmask 255.255.248.0 {
    range 192.181.0.2 192.181.7.254;
    option routers 192.181.0.1;
    option broadcast-address 192.181.7.255;
    option domain-name-servers 192.181.15.122;
    default-lease-time 180;
    max-lease-time 5760;
}

# A3
subnet 192.181.8.0 netmask 255.255.252.0 {
    range 192.181.8.3 192.181.11.254;
    option routers 192.181.8.1;
    option broadcast-address 192.181.11.255;
    option domain-name-servers 192.181.15.122;
    default-lease-time 180;
    max-lease-time 5760;
}

# A4
subnet 192.181.15.108 netmask 255.255.255.252 {
}

# A5
subnet 192.181.15.112 netmask 255.255.255.252 {
}

# A6
subnet 192.181.15.116 netmask 255.255.255.252 {
}

# A7
subnet 192.181.12.0 netmask 255.255.254.0 {
    range 192.181.12.2 192.181.13.254;
    option routers 192.181.12.1;
    option broadcast-address 192.181.13.255;
    option domain-name-servers 192.181.15.122;
    default-lease-time 180;
    max-lease-time 5760;
}

# A8
subnet 192.181.15.128 netmask 255.255.255.128 {
    range 192.181.15.131 192.181.15.254;
    option routers 192.181.15.129;
    option broadcast-address 192.181.15.255;
    option domain-name-servers 192.181.15.122;
    default-lease-time 180;
    max-lease-time 5760;
}

# A9
subnet 192.181.15.120 netmask 255.255.255.252 {
}

# A10
subnet 192.181.15.124 netmask 255.255.255.252 {
}
```

-   isc-dhcp-server

```sh
INTERFACESv4="eth0"
```

**Fern, Himmel, Frieren, Aura, Heiter (DHCP Relay)**

-   isc-dhcp-relay

```sh
SERVERS="192.181.15.126"
INTERFACES="eth0 eth2"
OPTIONS=
```

-   sysctl.conf

```sh
net.ipv4.ip_forward=1
```

## Soal Nomor 1

Agar topologi yang kalian buat dapat mengakses keluar, kalian diminta untuk mengkonfigurasi Aura menggunakan iptables, tetapi tidak ingin menggunakan MASQUERADE.

**Penyelesaian:**

-   **Aura**

```sh
ETH0_IP=$(ip -4 addr show eth0 | grep -oP '(?<=inet\s)\d+(\.\d+){3}')

iptables -t nat -A POSTROUTING -o eth0 -j SNAT --to-source $ETH0_IP -s 192.181.0.0/20
```

**Keterangan:**

-   `ip` : menampilkan informasi konfigurasi antarmuka `eth0`.
-   `grep` : digunakan untuk mengekstrak alamat IPv4 dari output tersebut.
-   `ETH0_IP`: variabel untuk menyimpan hasilnya.
-   `-t nat` : menentukan tabel iptables yang digunakan (dalam hal ini, tabel `nat`).
-   `A POSTROUTING` : menambahkan aturan pada chain POSTROUTING setelah paket meninggalkan antarmuka.
-   `o eth0` : menentukan antarmuka keluar (outbound) sebagai `eth0`.
-   `j SNAT` : menentukan tindakan yang akan diambil, yaitu melakukan `SNAT`.
-   `--to-source $ETH0_IP` : Mengatur alamat sumber yang akan digunakan dalam `SNAT`, yang dalam hal ini diambil dari variabel `ETH0_IP`.
-   `s 192.181.0.0/20` : Memilih paket-paket yang berasal dari subnet `192.181.0.0/20` untuk dikenakan `SNAT`.

**Output:**

![nomor1](https://cdn.discordapp.com/attachments/702797283795927123/1184519915374395413/image.png?ex=658c4523&is=6579d023&hm=ea0bafb85c54d042cebd0b5883da419a3c5b4a0fb52dd77452a2b669a45ad122&)

Note: semua node bisa melakukan `ping google.com`

## Soal Nomor 2

Kalian diminta untuk melakukan drop semua TCP dan UDP kecuali port 8080 pada TCP.

**Penyelesaian:**

-   **GrobeForest (512 Host)**

```sh
iptables -A INPUT -p tcp ! --dport 8080 -j DROP
iptables -A INPUT -p tcp --dport 8080 -j ACCEPT
iptables -A INPUT -p udp -s 192.181.0.0/20 -j DROP
```

**Keterangan:**

-   `A INPUT` : menambahkan aturan pada chain `INPUT` (paket yang menuju sistem itu sendiri).
-   `-p tcp` : menentukan bahwa aturan ini berlaku untuk protokol `TCP`.
-   `-p udp` : Menentukan bahwa aturan ini berlaku untuk protokol UDP.
-   `--dport 8080` : menentukan bahwa aturan ini akan diterapkan pada paket yang menuju port 8080.
-   `! --dport 8080` : menentukan bahwa aturan ini akan diterapkan pada semua port kecuali port 8080.
-   `-j DROP` : menentukan bahwa paket yang sesuai dengan aturan ini akan ditolak (DROP).
-   `-j ACCEPT` : menentukan bahwa paket yang sesuai dengan aturan ini akan diterima (ACCEPT).
-   `-s 192.181.0.0/20` : menentukan bahwa aturan ini akan diterapkan pada paket yang berasal dari subnet `192.181.0.0/20`.

**Output:**

-   Koneksi port tcp port 8080:

![nomor2a](https://cdn.discordapp.com/attachments/702797283795927123/1184383905118294068/image.png?ex=658bc677&is=65795177&hm=b79cb99f3e240ed892be8b20e2e879a5d1a6c3e2c584aba5a479135c513d0aee&)

-   Koneksi port tcp port lain (9000):

![nomor2b](https://cdn.discordapp.com/attachments/702797283795927123/1184384118507700244/image.png?ex=658bc6aa&is=657951aa&hm=a6ac02ecd05e5bb885952f3b18ff079aeaca0cf5b97654f0fca9a0e03f77b88f&)

-   Koneksi port udp port 8080:

![nomor2c](https://cdn.discordapp.com/attachments/702797283795927123/1184384807715745822/image.png?ex=658bc74e&is=6579524e&hm=061a32c8887b489e7dafa87486030885803dfae2854eca3839c84137d757aea4&)

## Soal Nomor 3

Kepala Suku North Area meminta kalian untuk membatasi DHCP dan DNS Server hanya dapat dilakukan ping oleh maksimal 3 device secara bersamaan, selebihnya akan di drop.

**Penyelesaian:**

-   **Revolte (DNS Server)**

```sh
iptables -A INPUT -m state --state ESTABLISHED,RELATED -j ACCEPT
iptables -A INPUT -p icmp -m connlimit --connlimit-above 3 --connlimit-mask 0 -j DROP
```

-   **Ritcher (DHCP Server)**

```sh
iptables -A INPUT -m state --state ESTABLISHED,RELATED -j ACCEPT
iptables -A INPUT -p icmp -m connlimit --connlimit-above 3 --connlimit-mask 0 -j DROP
```

**Keterangan:**

-   `-m state --state ESTABLISHED,RELATED` : menggunakan modul `state` untuk memeriksa status koneksi. Aturan ini mengizinkan paket-paket yang terkait dengan koneksi yang sudah terbentuk atau terkait dengan koneksi yang sedang berlangsung (misalnya, paket yang merupakan bagian dari koneksi TCP yang sudah terbentuk).
-   `-p icmp` : menentukan bahwa aturan ini berlaku untuk paket ICMP (misalnya, ping).
-   `-m connlimit --connlimit-above 3 --connlimit-mask 0`: Menggunakan modul `connlimit` untuk membatasi jumlah koneksi ICMP. Aturan ini menolak paket-paket ICMP jika jumlah koneksi ICMP dari satu alamat IP melebihi 3 dalam waktu yang sama.

**Output:**

-   Ping ke Revolte (DNS Server) ip `192.181.15.126`:

![nomor3a](https://cdn.discordapp.com/attachments/702797283795927123/1184372486616391700/image.png?ex=658bbbd5&is=657946d5&hm=922c426f986852d0e86c9c036d91e0d431e06dc67405a6704be124ba99334a5a&)

-   Ping ke Ritcher (DHCP Server) ip `192.181.15.122`:

![nomor3b](https://cdn.discordapp.com/attachments/702797283795927123/1184373143918366750/image.png?ex=658bbc72&is=65794772&hm=9871f9274293647a11bc6dbea22edaf2ad36fd3b9bbf0cd1302724e516abf5d1&)

## Soal Nomor 4, 5, 6, 8

**Nomor 4**
Lakukan pembatasan sehingga koneksi SSH pada Web Server hanya dapat dilakukan oleh masyarakat yang berada pada GrobeForest.

**Nomor 5**
Selain itu, akses menuju WebServer hanya diperbolehkan saat jam kerja yaitu Senin-Jumat pada pukul 08.00-16.00.

**Nomor 6**
Lalu, karena ternyata terdapat beberapa waktu di mana network administrator dari WebServer tidak bisa stand by, sehingga perlu ditambahkan rule bahwa akses pada hari Senin - Kamis pada jam 12.00 - 13.00 dilarang (istirahat maksi cuy) dan akses di hari Jumat pada jam 11.00 - 13.00 juga dilarang (maklum, Jumatan rek).

**Nomor 8**
Karena berbeda koalisi politik, maka subnet dengan masyarakat yang berada pada Revolte dilarang keras mengakses WebServer hingga masa pencoblosan pemilu kepala suku 2024 berakhir. Masa pemilu (hingga pemungutan dan penghitungan suara selesai) kepala suku bersamaan dengan masa pemilu Presiden dan Wakil Presiden Indonesia 2024.

**Penyelesaian:**

-   **Sein dan Stark (Web Server)**

```sh
# IP Subnet dari Revolte
REVOLTE_SUBNET="192.181.15.124/30"

MULAI_MASA_PEMILU=$(date -d "2023-10-19T00:00" +"%Y-%m-%dT%H:%M")

SELESAI_MASA_PEMILU=$(date -d "2024-02-15T00:00" +"%Y-%m-%dT%H:%M")

# Atur waktu untuk masa pemilu
iptables -A INPUT -p tcp -s $REVELTE_SUBNET --dport 80 -m time --datestart "$MULAI_MASA_PEMILU" --datestop "$SELESAI_MASA_PEMILU" -j DROP

iptables -A INPUT -p tcp --dport 22 -m time --weekdays Mon,Tue,Wed,Thu --timestart 12:00 --timestop 13:00 -j DROP
iptables -A INPUT -p tcp --dport 22 -m time --weekdays Fri --timestart 11:00 --timestop 13:00 -j DROP
iptables -A INPUT -p tcp --dport 22 -m time --weekdays Mon,Tue,Wed,Thu,Fri --timestart 08:00 --timestop 16:00 -j ACCEPT
iptables -A INPUT -p tcp --dport 22 -j DROP
```

**Keterangan: (Nomor 4)**

```sh
iptables -A INPUT -p tcp --dport 22 -j ACCEPT
iptables -A INPUT -p tcp --dport 22 -j DROP
```

-   `--dport 22` : menentukan bahwa aturan ini akan diterapkan pada paket yang menuju port 22 (SSH).

**Keterangan: (Nomor 5)**

Tambahkan aturan pada `iptables -A INPUT -p tcp --dport 22 -j ACCEPT` menjadi:

```sh
iptables -A INPUT -p tcp --dport 22 -m time --weekdays Mon,Tue,Wed,Thu,Fri --timestart 08:00 --timestop 16:00 -j ACCEPT
```

-   mengizinkan akses SSH pada hari kerja (Senin hingga Jumat) pada jam kantor (08:00 - 16:00).

**Keterangan: (Nomor 6)**

```sh
iptables -A INPUT -p tcp --dport 22 -m time --weekdays Mon,Tue,Wed,Thu --timestart 12:00 --timestop 13:00 -j DROP
iptables -A INPUT -p tcp --dport 22 -m time --weekdays Fri --timestart 11:00 --timestop 13:00 -j DROP
```

-   menetapkan pembatasan waktu untuk akses SSH pada hari kerja (Senin hingga Kamis) dan Jumat pada waktu-waktu tertentu. SSH tidak diizinkan selama jam makan dan jumatan (12:00 - 13:00 pada hari kerja dan 11:00 - 13:00 pada Jumat).

**Output:**

-   Nomor 4:

![nomor4](https://cdn.discordapp.com/attachments/702797283795927123/1184383462887657472/image.png?ex=658bc60e&is=6579510e&hm=3143f505279ae746b83eab65b994b2a85ac5a883fbf2f6988afd0b3df425f861&)

Menggunakan `nmap 192.181.8.2 22` di **GrobeForest** dihasilkan `open` dan **LaubHills** dihasilkan `filtered`.

-   Nomor 5:

![nomor5a](https://cdn.discordapp.com/attachments/702797283795927123/1184390557309620274/image.png?ex=658bcca9&is=657957a9&hm=dadcd9093c3f27f9173838d50265eb654897f68c9ef8d6c59285d7e9d179acf3&)

![nomor5b](https://cdn.discordapp.com/attachments/702797283795927123/1184390820124696708/image.png?ex=658bcce8&is=657957e8&hm=e1e06856d2c0cd38493283f99568d5a3c644a9c02bcf5f35e2bee88a49846e5f&)

Menggunakan `nmap 192.181.8.2 22` di **GrobeForest** pada hari `Rabu` dihasilkan `open` dan pada hari `Sabtu` dihasilkan `filtered`.

-   Nomor 6:

![nomor6a](https://cdn.discordapp.com/attachments/702797283795927123/1184402231844409394/image.png?ex=658bd789&is=65796289&hm=9e9187df1ca97c2e50d181c230e680f1da2826ab1ee5154cb07ce948d1d53b6a&)

![nomor6b](https://cdn.discordapp.com/attachments/702797283795927123/1184402043344003183/image.png?ex=658bd75c&is=6579625c&hm=f56a820f5c641643aaf012556b7e6b586f5de0da8aeea90711a7e8f41db41c21&)

Pada hari Kamis pukul `11.30` dihasilkan `open` dan pada pukul `12.30` dihasilkan `filtered`.

![nomor6c](https://cdn.discordapp.com/attachments/702797283795927123/1184403143308611605/image.png?ex=658bd862&is=65796362&hm=5a5a0229f4fc5cfdaa93f48d31b6ac2e2b00094f473f27c788eba0bd18536b66&)

![nomor6d](https://cdn.discordapp.com/attachments/702797283795927123/1184402898097016853/image.png?ex=658bd828&is=65796328&hm=4aee4e52d07da7ef7904da7c5aaacc0528ee120802bd35dd9d6f239c561c5a3d&)

Pada hari Jumat pukul `13.30` dihasilkan `open` dan pada pukul `11.30` dihasilkan `filtered`.

-   Nomor 8:

## Soal Nomor 7

Karena terdapat 2 WebServer, kalian diminta agar setiap client yang mengakses Sein dengan Port 80 akan didistribusikan secara bergantian pada Sein dan Stark secara berurutan dan request dari client yang mengakses Stark dengan port 443 akan didistribusikan secara bergantian pada Sein dan Stark secara berurutan.

**Penyelesaian:**

**Keterangan:**

**Output:**

## Soal Nomor 9

Sadar akan adanya potensial saling serang antar kubu politik, maka WebServer harus dapat secara otomatis memblokir alamat IP yang melakukan scanning port dalam jumlah banyak (maksimal 20 scan port) di dalam selang waktu 10 menit. (clue: test dengan nmap)

**Penyelesaian:**

**Keterangan:**

**Output:**

## Soal Nomor 10

Karena kepala suku ingin tau paket apa saja yang di-drop, maka di setiap node server dan router ditambahkan logging paket yang di-drop dengan standard syslog level.

**Penyelesaian:**

**Keterangan:**

**Output:**
