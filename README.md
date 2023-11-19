# Jarkom-Modul-3-A06-2023

## Group Member

| NRP        | Name                        |
| ---------- | --------------------------- |
| 5025211057 | Salsabila Fatma Aripa       |
| 5025211254 | Yusna Millaturrosyidah      |

## Daftar Isi
- [Topologi](#topologi)
- [Config](#config)
- [Soal 1](#soal-1)
	- [Penyelesaian soal 1](#penyelesaian-soal-1)
- [Soal 2](#soal-2)
	- [Penyelesaian soal 2](#penyelesaian-soal-2)
- [Soal 3](#soal-3)
	- [Penyelesaian soal 3](#penyelesaian-soal-3)
- [Soal 4](#soal-4)
	- [Penyelesaian soal 4](#penyelesaian-soal-4)
- [Soal 5](#soal-5)
	- [Penyelesaian soal 5](#penyelesaian-soal-5)
- [Soal 6](#soal-6)
	- [Penyelesaian soal 6](#penyelesaian-soal-6)
- [Soal 7](#soal-7)
	- [Penyelesaian soal 7](#penyelesaian-soal-7)
- [Soal 8](#soal-8)
	- [Penyelesaian soal 8](#penyelesaian-soal-8)
- [Soal 9](#soal-9)
	- [Penyelesaian soal 9](#penyelesaian-soal-9)
- [Soal 10](#soal-10)
	- [Penyelesaian soal 10](#penyelesaian-soal-10)
- [Soal 11](#soal-11)
	- [Penyelesaian soal 11](#penyelesaian-soal-11)
- [Soal 12](#soal-12)
	- [Penyelesaian soal 12](#penyelesaian-soal-2)
- [Soal 13](#soal-13)
	- [Penyelesaian soal 13](#penyelesaian-soal-13)
- [Soal 14](#soal-14)
	- [Penyelesaian soal 14](#penyelesaian-soal-14)
- [Soal 15](#soal-15)
	- [Penyelesaian soal 15](#penyelesaian-soal-15)
- [Soal 16](#soal-16)
	- [Penyelesaian soal 16](#penyelesaian-soal-16)
- [Soal 17](#soal-17)
	- [Penyelesaian soal 17](#penyelesaian-soal-17)
- [Soal 18](#soal-18)
	- [Penyelesaian soal 18](#penyelesaian-soal-18)
- [Soal 19](#soal-19)
	- [Penyelesaian soal 19](#penyelesaian-soal-19)
- [Soal 20](#soal-20)
	- [Penyelesaian soal 20](#penyelesaian-soal-20)
- [Kendala](#Kendala)

## Topologi
<img width="579" alt="topologi modul 3" src="https://github.com/yusnaaaaa/Jarkom-Modul-3-A06-2023/assets/91377793/bb389c55-c592-4d7c-a8a4-0585d0638a96">

## Config
Membuat konfigurasi pada setiap node yang ada sebagai berikut : 
#### Aura (DHCP Relay)
```
auto eth0
iface eth0 inet dhcp
iptables -t nat -A POSTROUTING -o eth0 -j MASQUERADE -s 10.2.0.0/16

auto eth1
iface eth1 inet static
	address 10.2.1.11
	netmask 255.255.255.0

auto eth2
iface eth2 inet static
	address 10.2.2.11
	netmask 255.255.255.0

auto eth3
iface eth3 inet static
	address 10.2.3.11
	netmask 255.255.255.0

auto eth4
iface eth4 inet static
	address 10.2.4.11
	netmask 255.255.255.0
```

#### Himmel (DHCP Server)
```
auto eth0
iface eth0 inet static
	address 10.2.1.2
	netmask 255.255.255.0
	gateway 10.2.1.11
```

#### Heiter (DNS Server)
```
auto eth0
iface eth0 inet static
	address 10.2.1.3
	netmask 255.255.255.0
	gateway 10.2.1.11
```

#### Denken (Database Server)
```
auto eth0
iface eth0 inet static
	address 10.2.2.2
	netmask 255.255.255.0
	gateway 10.2.2.11
```

#### Eisen (Load Balancer)
```
auto eth0
iface eth0 inet static
	address 10.2.2.3
	netmask 255.255.255.0
	gateway 10.2.2.11
```

#### Laravel Worker
Frieren
```
auto eth0
iface eth0 inet dhcp
hwaddress ether 7a:6d:c7:77:9b:fb
```

Flamme
```
auto eth0
iface eth0 inet dhcp
hwaddress ether 3e:26:cc:9e:a3:1e
```

Fern
```
auto eth0
iface eth0 inet dhcp
hwaddress ether 82:69:33:8f:d8:e1
```

#### PHP Worker
Lawine
```
auto eth0
iface eth0 inet dhcp
hwaddress ether 02:0f:9c:37:c7:60
```

Linie
```
auto eth0
iface eth0 inet dhcp
hwaddress ether aa:f6:88:e0:1c:73
```

Lugner
```
auto eth0
iface eth0 inet dhcp
hwaddress ether aa:d4:14:04:41:9d
```

#### Client
Sein, Stark, Revolte, Richter
```
auto eth0
iface eth0 inet dhcp
```

## Soal 1
Setelah mengalahkan Demon King, perjalanan berlanjut. Kali ini, kalian diminta untuk melakukan register domain berupa riegel.canyon.yyy.com untuk worker Laravel dan granz.channel.yyy.com untuk worker PHP (0) mengarah pada worker yang memiliki IP [prefix IP].x.1.
Lakukan konfigurasi sesuai dengan peta yang sudah diberikan.

### Penyelesaian soal 1
Lakukan konfigurasi pada Heiter (DNS Server), tambahkan command seperti dibawah ini : 

```
echo nameserver 192.168.122.1 > etc/resolv.conf
 
apt-get update

apt-get install bind9 -y

mkdir /etc/bind/jarkom

echo ‘
# Mendefinisikan Domain

zone "riegel.canyon.A06.com" {
type master;
file "/etc/bind/jarkom/riegel.canyon.A06.com";
};
zone "granz.channel.A06.com" {
type master;
file "/etc/bind/jarkom/granz.channel.A06.com";
};
zone "1.2.10.in-addr.arpa" {
type master;
file "/etc/bind/sites/1.2.10.in-addr.arpa";
};
‘ > /etc/bind/named.conf.local

cp named.conf.local /etc/bind/

cp /etc/bind/db.local /etc/bind/jarkom/riegel.canyon.A06.com

cp /etc/bind/db.local /etc/bind/jarkom/granz.channel.A06.com

echo ‘
;
; BIND data file for local loopback interface
;
$TTL    604800
@       IN      SOA     riegel.canyon.A06.com. root.riegel.canyon.A06.com. (
         2		      	; Serial
         604800         	; Refresh
         86400         	; Retry
         2419200         	; Expire
        604800 )       ; Negative Cache TTL
;
@       IN      NS     	    riegel.canyon.A06.com.
@       IN      A       	    10.2.2.3 	
www   IN      CNAME       riegel.canyon.A06.com.
‘ > /etc/bind/jarkom/riegel.canyon.A06.com

echo ‘
;
; BIND data file for local loopback interface
;
$TTL    604800
@       IN      SOA     granz.channel.A06.com. root.granz.channel.A06.com. (
         2		      	; Serial
         604800         	; Refresh
         86400         	; Retry
         2419200         	; Expire
        604800 )       ; Negative Cache TTL
;
@       IN      NS     	    granzchannel.A06.com.
@       IN      A       	    10.2.2.3
www   IN      CNAME       granz.channel.A06.com.
‘ > /etc/bind/jarkom/granz.channel.A06.com

service bind9 restart

```

#### Hasil
<img width="456" alt="no1" src="https://github.com/yusnaaaaa/Jarkom-Modul-3-A06-2023/assets/91377793/22863898-7078-4bb7-8439-64f34a8a68a4">

## Soal 2
Client yang melalui Switch3 mendapatkan range IP dari [prefix IP].3.16 - [prefix IP].3.32 dan [prefix IP].3.64 - [prefix IP].3.80

### Penyelesaian soal 2
Pertama yaitu melakukan konfigurasi pada DHCP Relay sebagai berikut : 
```
echo '
SERVER="10.2.1.2"
INTERFACES="eth1 eth2 eth3 eth4"
' > /etc/default/isc-dhcp-relay

echo '
net.ipv4.ip_forward=1
' > /etc/sysctl.conf

service isc-dhcp-relay start
```

Kemudian, lakukan konfigurasi juga pada DHCP Server sebagai berikut : 
```
echo '
INTERFACESv4="eth0"
INTERFACESv6=""
' > /etc/default/isc-dhcp-server

echo '
subnet 10.2.1.0 netmask 255.255.255.0 {
}

subnet 10.2.2.0 netmask 255.255.255.0 {
}

subnet 10.2.3.0 netmask 255.255.255.0 {
    range 10.2.3.16 10.2.3.32;
    range 10.2.3.64 10.2.3.80;
    option routers 10.2.3.11;
    option broadcast-address 10.2.3.255;
    option domain-name-servers 10.2.1.3;
}
' > etc/dhcp/dhcpd.conf

```

## Soal 3
Client yang melalui Switch4 mendapatkan range IP dari [prefix IP].4.12 - [prefix IP].4.20 dan [prefix IP].4.160 - [prefix IP].4.168

### Penyelesaian soal 3
Tambahkan konfigurasi pada file `/etc/dhcp/dhcpd.conf` pada DHCP Server sebagai berikut : 
```
echo '
subnet 10.2.4.0 netmask 255.255.255.0 {
    range 10.2.4.12 10.2.4.32;
    range 10.2.4.160 10.2.4.168;
    option routers 10.2.4.11;
    option broadcast-address 10.2.4.255;
    option domain-name-servers 10.2.1.3;
}
' >> /etc/dhcp/dhcpd.conf

service isc-dhcp-server restart
```

## Soal 4
Client mendapatkan DNS dari Heiter dan dapat terhubung dengan internet melalui DNS tersebut

### Penyelesaian soal 4
Menambahkan forwarders pada file konfig /etc/bind/named.conf.options, untuk menentukan server DNS eksternal yang akan digunakan sebagai forwarders oleh server BIND9.
```
echo ‘
options {
        directory "/var/cache/bind";

        forwarders {
                192.168.122.1;
        };

      // dnssec-validation auto;
        allow-query{any;};
        auth-nxdomain no;
        listen-on-v6 { any; };
};
‘ > /etc/bind/named.conf.local

Service bind9 restart
```

## Soal 5
Lama waktu DHCP server meminjamkan alamat IP kepada Client yang melalui Switch3 selama 3 menit sedangkan pada client yang melalui Switch4 selama 12 menit. Dengan waktu maksimal dialokasikan untuk peminjaman alamat IP selama 96 menit 

### Penyelesaian soal 5
Untuk mengatasi kebutuhan leasing time yang berbeda antara Switch3 dan Switch4 dalam jaringan, kita akan menggunakan fungsi default-lease-time dan max-lease-time pada server DHCP. Pada Switch3, durasi peminjaman IP selama 3 menit maka akan diatur menjadi 180 detik, sedangkan pada Switch4, durasi peminjaman IP selama 12 menit maka durasinya akan menjadi 720 detik. Selain itu, max-lease-time akan diatur ke 5760 detik untuk memastikan batasan waktu peminjaman IP tidak melebihi 96 menit.
```
echo ‘
subnet 10.2.1.0 netmask 255.255.255.0 {
}

subnet 10.2.2.0 netmask 255.255.255.0 {
}

subnet 10.2.3.0 netmask 255.255.255.0 {
    range 10.2.3.16 10.2.3.32;
    range 10.2.3.64 10.2.3.80;
    option routers 10.2.3.11;
    option broadcast-address 10.2.3.255;
    option domain-name-servers 10.2.1.3;
    default-lease-time 180;
    max-lease-time 5760;
}

subnet 10.2.4.0 netmask 255.255.255.0 {
    range 10.2.4.12 10.2.4.32;
    range 10.2.4.160 10.2.4.168;
    option routers 10.2.4.11;
    option broadcast-address 10.2.4.255;
    option domain-name-servers 10.2.1.3;
    default-lease-time 720;
    max-lease-time 5760;
}
‘ > /etc/dhcp/dhcpd.conf

service isc-dhcp-server restart
```

#### Hasil 
- IP DHCP pada Client dengan Switch 3
<img width="436" alt="dhcp switch3" src="https://github.com/yusnaaaaa/Jarkom-Modul-3-A06-2023/assets/91377793/ef5833a3-d38b-4dca-bf9d-f5b71392410d">

- IP DHCP pada Client dengan Switch 4
<img width="410" alt="dhcp switch 4" src="https://github.com/yusnaaaaa/Jarkom-Modul-3-A06-2023/assets/91377793/59494ea5-2b77-4a54-ae46-ca5ba04fc070">

## Soal 6

### Penyelesaian soal 6

## Soal 7

Kepala suku dari Bredt Region memberikan resource server sebagai berikut:
- Lawine, 4GB, 2vCPU, dan 80 GB SSD.
- Linie, 2GB, 2vCPU, dan 50 GB SSD.
- Lugner 1GB, 1vCPU, dan 25 GB SSD.
aturlah agar Eisen dapat bekerja dengan maksimal, lalu lakukan testing dengan 1000 request dan 100 request/second.

### Penyelesaian soal 7

Pertama yaitu lakukan instalasi dependencies yang dibutuhkan sebagai berikut : 
```
echo 'nameserver 10.2.1.3' > /etc/resolv.conf
apt-get update
apt-get install apache2-utils -y
apt-get install nginx -y
apt-get install lynx -y

service nginx start
```
Kemudian lakukan konfigurasi pada nginx di node Eisen (Load Balancer) seperti dibawah ini : 
```
cp /etc/nginx/sites-available/default /etc/nginx/sites-available/lb_php

echo ' 
upstream worker {
    server 10.2.3.1;
    server 10.2.3.2;
    server 10.2.3.3;
}

server {
    listen 80;
    server_name granz.channel.A06.com www.granz.channel.A06.com;

    root /var/www/html;

    index index.html index.htm index.nginx-debian.html;

    server_name _;

    location / {
        proxy_pass http://worker;
    }
} ' > /etc/nginx/sites-available/lb_php

ln -s /etc/nginx/sites-available/lb_php /etc/nginx/sites-enabled/
rm /etc/nginx/sites-enabled/default

service nginx restart
``` 

Lalu jalankan perintah pada client Richter seperti dibawah ini : 
```
ab -n 1000 -c 100 http://www.granz.channel.A06.com/
```
![Screenshot 2023-11-16 185921](https://github.com/yusnaaaaa/Jarkom-Modul-3-A06-2023/assets/114417418/c0714f99-bc23-4fc0-b0d1-d50de7373318)

![Screenshot 2023-11-16 190052](https://github.com/yusnaaaaa/Jarkom-Modul-3-A06-2023/assets/114417418/d774128a-78e3-4190-8024-697ba13a8a1e)

![Screenshot 2023-11-16 190119](https://github.com/yusnaaaaa/Jarkom-Modul-3-A06-2023/assets/114417418/d366c465-a0f1-458c-8dcc-4fa4af16ddf8)


## Soal 8

Karena diminta untuk menuliskan grimoire, buatlah analisis hasil testing dengan 200 request dan 10 request/second masing-masing algoritma Load Balancer dengan ketentuan sebagai berikut:
- Nama Algoritma Load Balancer.
- Report hasil testing pada Apache Benchmark.
- Grafik request per second untuk masing masing algoritma.
- Analisis.

### Penyelesaian soal 8

Melakukan pengecekan dengan algoritma load balancer dengan
Round Robin
```
upstream mynode {
 	server 10.2.3.1;
 	server 10.2.3.2;
 	server 10.2.3.3;
 }
```
Least Connection
```
upstream mynode {
    least_conn;
    	server 10.2.3.1;
 	server 10.2.3.2;
 	server 10.2.3.3;

}
```
IP Hash
```
 upstream mynode {
 	ip_hash;
 	server 10.2.3.1;
 	server 10.2.3.2;
 	server 10.2.3.3;
 }
```
Generic Hash
```
 upstream mynode {
 	hash $request_uri consistent;
 	server 10.2.3.1;
 	server 10.2.3.2;
 	server 10.2.3.3;
 }
```
Setelah itu kita lakukan testing di client dengan perintah
```
ab -n 200 -c 10 http://www.granz.channel.A02.com/ 
```
Report hasil testing dapat dilihat pada laporan di link berikut [Grimore](https://drive.google.com/file/d/1QBCYDKbpsfawwd-AT4dsxJNzb1bGn7cC/view?usp=sharing)

Round Robin

![roundrobin](https://github.com/yusnaaaaa/Jarkom-Modul-3-A06-2023/assets/114417418/6e6b98e2-66f7-4e3d-8f71-9d0116c17790)

Least Connection

![lastconnection](https://github.com/yusnaaaaa/Jarkom-Modul-3-A06-2023/assets/114417418/c347d402-d067-4c0b-952b-bb47363e6dd8)

IP Hash

![iphash](https://github.com/yusnaaaaa/Jarkom-Modul-3-A06-2023/assets/114417418/1cbb5943-f0b0-40d2-a93c-35f36e4e0490)

Generic Hash

![generic](https://github.com/yusnaaaaa/Jarkom-Modul-3-A06-2023/assets/114417418/05b1739a-34f8-4e0d-b54a-5a8198a54f14)

Grafik

![1](https://github.com/yusnaaaaa/Jarkom-Modul-3-A06-2023/assets/114417418/84c59006-deb6-4c39-b11f-d459337228ca)

## Soal 9

Dengan menggunakan algoritma Round Robin, lakukan testing dengan menggunakan 3 worker, 2 worker, dan 1 worker sebanyak 100 request dengan 10 request/second, kemudian tambahkan grafiknya pada grimoire.

### Penyelesaian soal 9

Melakukan command berikut pada client
```
ab -n 100 -c 10 http://www.granz.channel.A06.com/ 
```
Setelah itu stop 1 worker untuk mengecek penggunaan 2 worker. Lalu lakukan command diatas lagi pada client.

Selanjutnya stop 1 worker lagi untuk mengecek penggunaan 1 worker. Lalu lakukan command diatas lagi pada client.

3 Worker

![3w](https://github.com/yusnaaaaa/Jarkom-Modul-3-A06-2023/assets/114417418/145a4781-d18b-44f0-894f-8cb4ca87588d)

2 Worker

![2w](https://github.com/yusnaaaaa/Jarkom-Modul-3-A06-2023/assets/114417418/ba415170-de57-4dbf-87e1-b1c254d656f2)

1 Worker

![1w](https://github.com/yusnaaaaa/Jarkom-Modul-3-A06-2023/assets/114417418/214ebcd4-5263-4ca2-a8d9-43aa740e0e57)

Grafik

![2](https://github.com/yusnaaaaa/Jarkom-Modul-3-A06-2023/assets/114417418/ce962545-0884-4c61-ac4f-412872bad132)

## Soal 10

Selanjutnya coba tambahkan konfigurasi autentikasi di LB dengan dengan kombinasi username: “netics” dan password: “ajkyyy”, dengan yyy merupakan kode kelompok. Terakhir simpan file “htpasswd” nya di /etc/nginx/rahasisakita/

### Penyelesaian soal 10

Pertama yaitu jalankan command dibawah ini satu persatu pada node Eisen (Load Balancer) : 
```
mkdir /etc/nginx/rahasisakita
htpasswd -c /etc/nginx/rahasisakita/htpasswd netics
```
Kemudian masukkan password sesuai perintah yaitu `ajkA06`

Lalu apabila telah menginputkan password dan re-type password, maka tambahkan command dibawah ini pada bagian setup nginx.
```
auth_basic "Restricted Content";
auth_basic_user_file /etc/nginx/rahasisakita/htpasswd;
```

Setelah itu kita dapat kembali menjalankan url `http://www.granz.channel.A06.com/` dan akan muncul tampilan seperti dibawah ini : 

![Screenshot (2884)](https://github.com/yusnaaaaa/Jarkom-Modul-3-A06-2023/assets/114417418/2342ad2a-d7b1-4f04-8c13-9c5c25950cde)

![Screenshot (2885)](https://github.com/yusnaaaaa/Jarkom-Modul-3-A06-2023/assets/114417418/becb9b3a-6d4f-4c2f-a31f-a640fe6b515d)

![Screenshot (2886)](https://github.com/yusnaaaaa/Jarkom-Modul-3-A06-2023/assets/114417418/ef74cbe1-992b-4c71-a3f5-521d63f8daac)

![Screenshot (2883)](https://github.com/yusnaaaaa/Jarkom-Modul-3-A06-2023/assets/114417418/3602b276-b9c3-46e2-aa9a-62d8eb4be87e)

## Soal 11

Lalu buat untuk setiap request yang mengandung /its akan di proxy passing menuju halaman `https://www.its.ac.id`.

### Penyelesaian soal 11
Tambahkan konfigurasi pada nginx seperti dibawah ini  : 
```
echo '
upstream worker {
    server 10.2.3.1;
    server 10.2.3.2;
    server 10.2.3.3;
}

server {
    listen 80;
    server_name granz.channel.A06.com www.granz.channel.A06.com;

    root /var/www/html;
    index index.html index.htm index.nginx-debian.html;

    location / {
        proxy_pass http://worker;
    }

    location ~ /its {
        proxy_pass https://www.its.ac.id;
        proxy_set_header Host www.its.ac.id;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
    }
}
' > /etc/nginx/sites-available/lb_php
```

Kemudian apabila mengakses endpoint yang mengandung "/its," perintah proxy_pass akan mengarahkan permintaan tersebut ke https://www.its.ac.id. Dengan demikian, saat melakukan uji coba dengan client Richter, dapat menggunakan perintah seperti dibawah ini : 
```
lynx www.granz.channel.A06.com/its
```
Maka akan muncul tampilan seperti dibawah ini : 

![Screenshot (2894)](https://github.com/yusnaaaaa/Jarkom-Modul-3-A06-2023/assets/114417418/2ec54699-4014-48f0-84d8-09675a1085f1)



## Soal 12

### Penyelesaian soal 12

## Soal 13

### Penyelesaian soal 13

## Soal 14

### Penyelesaian soal 14

## Soal 15

### Penyelesaian soal 15

## Soal 16

### Penyelesaian soal 16

## Soal 17

### Penyelesaian soal 17

## Soal 18

### Penyelesaian soal 18

## Soal 19

### Penyelesaian soal 19

## Soal 20

### Penyelesaian soal 20
