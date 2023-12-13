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

- **Pembagian rute:**

![bjir1](https://github.com/ddedida/Jarkom-Modul-5-B06-2023/assets/108203648/4a17f030-eda4-4199-ad57-dd583fdc3269)

![image](https://github.com/ddedida/Jarkom-Modul-5-B06-2023/assets/108203648/7968bc9a-c2cb-40db-bbac-f9a8ee659fde)

- **Tree VLSM:**

<img width="1826" alt="bjir" src="https://github.com/ddedida/Jarkom-Modul-5-B06-2023/assets/108203648/7b3100e5-bad2-4dce-9ebc-2ca9b27aaaa0">

#### Kemudian buatlah rute sesuai dengan pembagian IP yang kalian lakukan:

![image](https://github.com/ddedida/Jarkom-Modul-5-B06-2023/assets/108203648/b72f7902-a130-4586-adfc-7dcf80626252)

Berikut merupakan [link](<[https://github.com/user/repo/blob/branch/other_file.md](https://docs.google.com/spreadsheets/d/18h_e6yaBEORnPLRlbLNUG6ELZ2ZwMwkHk0R6c12TuhY/edit?usp=sharing)https://docs.google.com/spreadsheets/d/18h_e6yaBEORnPLRlbLNUG6ELZ2ZwMwkHk0R6c12TuhY/edit?usp=sharing>) spreadsheet untuk pembagian ip masing-masing node.

**Konfigurasi Subnetting (setiap node) dan Routing (Aura, Frieren, dan Himmel):**

- Aura

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

- Heiter

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

- TurkRegion (1022 Host)

```sh
# Static config for eth0
auto eth0
iface eth0 inet dhcp
	gateway 192.181.0.1

up echo nameserver 192.168.122.1 > /etc/resolv.conf
```

- Sein (Web Server)

```sh
# Static config for eth0
auto eth0
iface eth0 inet static
	address 192.181.8.2
	netmask 255.255.252.0
	gateway 192.181.8.1

up echo nameserver 192.168.122.1 > /etc/resolv.conf
```

- GrobeForest (512 Host)

```sh
# Static config for eth0
auto eth0
iface eth0 inet dhcp
        gateway 192.181.8.1

up echo nameserver 192.168.122.1 > /etc/resolv.conf
```

- Frieren

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

- Stark (Web Server)

```sh
# Static config for eth0
auto eth0
iface eth0 inet static
	address 192.181.15.114
	netmask 255.255.255.252
	gateway 192.181.15.113

up echo nameserver 192.168.122.1 > /etc/resolv.conf
```

- Himmel

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

- LaubHills (255 Host)

```sh
# Static config for eth0
auto eth0
iface eth0 inet dhcp
	gateway 192.181.12.1

up echo nameserver 192.168.122.1 > /etc/resolv.conf
```

- SchwerMountain (64 Host)

```sh
# Static config for eth0
auto eth0
iface eth0 inet dhcp
	gateway 192.181.15.129

up echo nameserver 192.168.122.1 > /etc/resolv.conf
```

- Fern

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

- Ritcher (DNS Server)

```sh
# Static config for eth0
auto eth0
iface eth0 inet static
	address 192.181.15.122
	netmask 255.255.255.252
	gateway 192.181.15.121

up echo nameserver 192.168.122.1 > /etc/resolv.conf
```

- Revolte (DHCP Server)

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

- dhcp.conf

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

- isc-dhcp-server

```sh
INTERFACESv4="eth0"
```

**Fern, Himmel, Frieren, Aura, Heiter (DHCP Relay)**

- isc-dhcp-relay

```sh
SERVERS="192.181.15.126"
INTERFACES="eth0 eth2"
OPTIONS=
```

- sysctl.conf

```sh
net.ipv4.ip_forward=1
```

## Soal Nomor 1
