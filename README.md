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
	- [Penyelesaian soal 12](#penyelesaian-soal-12)
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
Pada masing-masing worker PHP, lakukan konfigurasi virtual host untuk website berikut dengan menggunakan php 7.3.

### Penyelesaian soal 6
Pertama yaitu lakukan instalasi dependencies yang dibutuhkan sebagai berikut : 
#### Pada semua Client
```
apt update
apt install lynx -y
apt install htop -y
apt install apache2-utils -y
apt install nginx -y
```

#### Pada semua PHP Worker
```
apt update
apt install nginx -y
service nginx start
apt-get install php php-fpm -y
```
Kemudian lakukan konfigurasi tambahan sebagai berikut untuk melakukan git clone pada file yang telah disediakan, sebelum itu silahkan masuk ke dalam directory `/var/www` didalam worker. kemudian lakukan command seperti dibawah ini : 
```
apt install git
git clone -b granz https://github.com/yusnaaaaa/JarkomPrak3-Dependencies
mv JarkomPrak3-Dependencies /var/www/granz.channel.A06.com
```

Lalu lakukan konfigurasi pada nginx seperti dibawah ini : 
```
cp /etc/nginx/sites-available/default /etc/nginx/sites-available/granz.channel.A06.com
ln -s /etc/nginx/sites-available/granz.channel.A06.com /etc/nginx/sites-enabled/
rm /etc/nginx/sites-enabled/default

echo 'server {
    listen 80;
    server_name _;

    root /var/www/granz.channel.A06.com;
    index index.php index.html index.htm;

    location / {
        try_files $uri $uri/ /index.php?$query_string;
    }

    location ~ \.php$ {
        include snippets/fastcgi-php.conf;
        fastcgi_pass unix:/run/php/php7.3-fpm.sock;  # Sesuaikan versi PHP dan socket
        fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
        include fastcgi_params;
    }
}' > /etc/nginx/sites-available/granz.channel.A06.com

service nginx restart
```
Setelah itu coba cek pada client dengan menggunakan command `lynx granz.channel.A06.com`

Apabila berhasil maka akan muncul tampilan seperti dibawah ini : 
<img width="960" alt="no 6" src="https://github.com/yusnaaaaa/Jarkom-Modul-3-A06-2023/assets/91377793/5b8e0cff-251d-4466-985e-50995ac0996e">


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

![pass1](https://github.com/yusnaaaaa/Jarkom-Modul-3-A06-2023/assets/114417418/efefe4bd-4911-4f69-ab4d-4517785666cd)

![pass2](https://github.com/yusnaaaaa/Jarkom-Modul-3-A06-2023/assets/114417418/64667e1b-98f5-46ae-98af-16c4e826fdd2)

![pass5](https://github.com/yusnaaaaa/Jarkom-Modul-3-A06-2023/assets/114417418/592b8b0b-7236-4640-ba88-44332a95c3a3)

![pass4](https://github.com/yusnaaaaa/Jarkom-Modul-3-A06-2023/assets/114417418/7872cfc2-89d0-447c-8f5c-5fd399ea9761)

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

![no11](https://github.com/yusnaaaaa/Jarkom-Modul-3-A06-2023/assets/114417418/3d917931-ac39-440b-80d8-5b2cb0a2f7a0)

## Soal 12
Selanjutnya LB ini hanya boleh diakses oleh client dengan IP [Prefix IP].3.69, [Prefix IP].3.70, [Prefix IP].4.167, dan [Prefix IP].4.168. (12) hint: (fixed in dulu clinetnya)

### Penyelesaian soal 12
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
        allow 10.2.3.69;
        allow 10.2.3.70;
        allow 10.2.4.167;
        allow 10.2.4.168;
        deny all;
        proxy_pass http://worker;
    }

    location /its {
        proxy_pass https://www.its.ac.id;
        proxy_set_header Host www.its.ac.id;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
    }
}
' > /etc/nginx/sites-available/lb_php
```
Dalam hal ini, hanya beberapa alamat IP tertentu yang diizinkan, sesuai dengan ketentuan yang telah ditetapkan. Semua alamat IP selain yang telah ditentukan akan ditolak. Untuk testing, kita dapat membuka klien yang diberikan alamat IP sebagai berikut : 
 10.2.3.69;
 10.2.3.70;
 10.2.4.167;
 10.2.4.168;

#### Hasil : 
- IP Deny
  <img width="960" alt="no12" src="https://github.com/yusnaaaaa/Jarkom-Modul-3-A06-2023/assets/91377793/b7fa3b15-72ed-4c17-98fd-5646a1ac0ed2">
  
- IP Allow
Dalam konteks pengaturan yang telah ada, yang membatasi akses hanya kepada beberapa alamat IP tertentu, kita ingin menambahkan izin akses untuk alamat IP 10.2.3.20.
```
location / {
    allow 10.2.3.20;
    allow 10.2.3.69;
    allow 10.2.3.70;
    allow 10.2.4.167;
    allow 10.2.4.168;
    deny all;
    proxy_pass http://worker;
}
```
Setelah berhasil, maka akan muncul tampilan seperti dibawah ini : 
<img width="960" alt="no12allow" src="https://github.com/yusnaaaaa/Jarkom-Modul-3-A06-2023/assets/91377793/b8f19a2a-05f2-41b3-8a77-99be7c7b9dcf">

## Soal 13
Semua data yang diperlukan, diatur pada Denken dan harus dapat diakses oleh Frieren, Flamme, dan Fern. 

### Penyelesaian soal 13

Pertama yaitu lakukan instalasi dependencies yang dibutuhkan sebagai berikut : 
```
echo 'nameserver 10.2.1.3' > /etc/resolv.conf
apt-get update
apt-get install mariadb-server -y
service mysql start
```

Lalu masuk ke node Denken (Database Server) untuk melakukan konfigurasi seperti dibawah ini : 
```
echo '
# This group is read both by the client and the server
# use it for options that affect everything
[client-server]

# Import all .cnf files from configuration directory
!includedir /etc/mysql/conf.d/
!includedir /etc/mysql/mariadb.conf.d/

# Options affecting the MySQL server (mysqld)
[mysqld]
skip-networking=0
skip-bind-address
' > /etc/mysql/my.cnf
```
Kemudian ganti [bind-address] pada /etc/mysql/mariadb.conf.d/50-server.cnf menjadi 0.0.0.0 seperti dibawah ini : 
```
cd /etc/mysql/mariadb.conf.d/50-server.cnf

# Changes
bind-address            = 0.0.0.0
```
Kemudian jalankan script dibwah ini : 
```
mysql -u root -p
Enter password:

CREATE USER 'kelompokA06'@'10.2.4.1' IDENTIFIED BY 'passwordA06';
CREATE USER 'kelompokA06'@'10.2.4.2' IDENTIFIED BY 'passwordA06';
CREATE USER 'kelompokA06'@'10.2.4.3' IDENTIFIED BY 'passwordA06';
CREATE USER 'kelompokA06'@'localhost' IDENTIFIED BY 'passwordA06';
CREATE DATABASE dbkelompokA06;

GRANT ALL PRIVILEGES ON *.* TO 'kelompokA06'@'10.2.4.1';
GRANT ALL PRIVILEGES ON *.* TO 'kelompokA06'@'10.2.4.2';
GRANT ALL PRIVILEGES ON *.* TO 'kelompokA06'@'10.2.4.3';
GRANT ALL PRIVILEGES ON *.* TO 'kelompokA06'@'localhost';

FLUSH PRIVILEGES;
```

Lalu, kita dapat melakukan testing pada salah satu Laravel Worker dengan perintah seperti dibawah ini : 
```
mariadb --host=10.2.2.2 --port=3306 --user=kelompokA06 --password=passwordA06 dbkelompokA06 -e "SHOW DATABASES;"
```
Setelah berhasil maka akan muncul tampilan seperti dibawah ini :

<img width="960" alt="no13" src="https://github.com/yusnaaaaa/Jarkom-Modul-3-A06-2023/assets/114417418/2d78c238-284f-4550-8d5b-5fec904a2538">

## Soal 14
Frieren, Flamme, dan Fern memiliki Riegel Channel sesuai dengan quest guide berikut. Jangan lupa melakukan instalasi PHP8.0 dan Composer

### Penyelesaian soal 14

Pertama yaitu melakukan instalasi dependencies yang dibutuhkan pada semua worker sebagai berikut : 
```
apt-get update
apt-get install -y lsb-release ca-certificates apt-transport-https
software-properties-common gnupg2
curl -sSLo /usr/share/keyrings/deb.sury.org-php.gpg https://packages.sury.org/php/apt.gpg
sh -c 'echo "deb [signed-by=/usr/share/keyrings/deb.sury.org-php.gpg] https://packages.sury.org/php/ $(lsb_release -sc) main" > /etc/apt/sources.list.d/php.list'
apt-get update
apt-get install php8.0-mbstring php8.0-xml php8.0-cli php8.0-common php8.0-intl php8.0-opcache php8.0-readline php8.0-mysql php8.0-fpm php8.0-curl unzip wget -y
apt-get install nginx -y
wget https://getcomposer.org/download/2.0.13/composer.phar
chmod +x composer.phar
mv composer.phar /usr/bin/composer
apt-get install git -y
git clone https://github.com/martuafernando/laravel-praktikum-jarkom
mv laravel-praktikum-jarkom /var/www/
```

Kemudian jalankan beberapa command berikut di file Laravel : 
```
Composer update
composer install
cp .env.example .env
php artisan migrate:fresh
php artisan db:seed --class=AiringsTableSeeder
php artisan key:generate
php artisan jwt:secret
```

Setelah itu lakukan konfigurasi pada file .env yang baru sebagai berikut : 
```
APP_NAME=Laravel
APP_ENV=local
APP_KEY=
APP_DEBUG=true
APP_URL=http://localhost

LOG_CHANNEL=stack
LOG_DEPRECATIONS_CHANNEL=null
LOG_LEVEL=debug

DB_CONNECTION=mysql
DB_HOST=10.2.2.2
DB_PORT=3306
DB_DATABASE=dbkelompokA06
DB_USERNAME=kelompokA06
DB_PASSWORD=passwordA06

BROADCAST_DRIVER=log
CACHE_DRIVER=file
FILESYSTEM_DISK=local
QUEUE_CONNECTION=sync
SESSION_DRIVER=file
SESSION_LIFETIME=120

MEMCACHED_HOST=127.0.0.1

REDIS_HOST=127.0.0.1
REDIS_PASSWORD=null
REDIS_PORT=6379

MAIL_MAILER=smtp
MAIL_HOST=mailpit
MAIL_PORT=1025
MAIL_USERNAME=null
MAIL_PASSWORD=null
MAIL_ENCRYPTION=null
MAIL_FROM_ADDRESS="hello@example.com"
MAIL_FROM_NAME="${APP_NAME}"

AWS_ACCESS_KEY_ID=
AWS_SECRET_ACCESS_KEY=
AWS_DEFAULT_REGION=us-east-1
AWS_BUCKET=
AWS_USE_PATH_STYLE_ENDPOINT=false

PUSHER_APP_ID=
PUSHER_APP_KEY=
PUSHER_APP_SECRET=
PUSHER_HOST=
PUSHER_PORT=443
PUSHER_SCHEME=https
PUSHER_APP_CLUSTER=mt1

VITE_PUSHER_APP_KEY="${PUSHER_APP_KEY}"
VITE_PUSHER_HOST="${PUSHER_HOST}"
VITE_PUSHER_PORT="${PUSHER_PORT}"
VITE_PUSHER_SCHEME="${PUSHER_SCHEME}"
VITE_PUSHER_APP_CLUSTER="${PUSHER_APP_CLUSTER}"
```


## Soal 15
Riegel Channel memiliki beberapa endpoint yang harus ditesting sebanyak 100 request dengan 10 request/second. Tambahkan response dan hasil testing pada grimoire.
a. POST /auth/register

### Penyelesaian soal 15

Pertama yaitu jalankan command pada semua worker sebagai berikut :
```
echo ‘
server {

    listen 80;

    root /var/www/laravel-praktikum-jarkom/public;

    index index.php index.html index.htm;
    server_name riegel.canyon.A06.com;

    location / {
            try_files $uri $uri/ /index.php?$query_string;
    }

    # pass PHP scripts to FastCGI server
    location ~ \.php$ {
    include snippets/fastcgi-php.conf;
    fastcgi_pass unix:/var/run/php/php8.0-fpm.sock;
    }

location ~ /\.ht {
            deny all;
    }

    error_log /var/log/nginx/implementasi_error.log;
    access_log /var/log/nginx/implementasi_access.log;
}’ > /etc/nginx/sites-available/implementasi
unlink /etc/nginx/sites-enabled/default
ln -s /etc/nginx/sites-available/implementasi /etc/nginx/sites-enabled/default
chown -R www-data.www-data /var/www/laravel-praktikum-jarkom/storage
service php8.0-fpm start
```

Lalu jalankan command pada node Eisen (Load Balancer) sebagai berikut : 
```
echo ‘
upstream laravel {
	server 10.2.4.1;
	server 10.2.4.2;
	server 10.2.4.3;
}

server {
	listen 80;
	server_name riegel.canyon.A06.com;
		location / {
                proxy_pass http://laravel;
                proxy_set_header    X-Real-IP $remote_addr;
                proxy_set_header    X-Forwarded-For $proxy_add_x_forwarded_for;
                proxy_set_header    Host $http_host;
        }
	error_log /var/log/nginx/lb_error.log;
access_log /var/log/nginx/lb_access.log;
}
’ > /etc/nginx/sites-available/lb-jarkom

unlink /etc/nginx/sites-enabled/default
ln -s /etc/nginx/sites-available/lb-jarkom /etc/nginx/sites-enabled/default
service nginx restart
```

Kemudian untuk melakukan testing, jalankan command berikut pada client : 
```
curl -X POST -d '{"username": "username", "password": "password"}' -H "Content-Type: application/json" http://riegel.canyon.A06.com/api/auth/register
```
Ketika telah berhasil akan muncul tampilan sebagai berikut :

![15curl](https://github.com/yusnaaaaa/Jarkom-Modul-3-A06-2023/assets/114417418/d554286b-26c9-4a8f-8163-00e92e537a0e)

Setelah itu jalankan dengan Apache benchmark seperti dibawah ini : 
```
ab -n 100 -c 10 -p <(curl -X POST -d '{"username": "username", "password": "password"}' -H "Content-Type: application/json" http://riegel.canyon.A06.com/api/auth/register
) -T "application/json" http://riegel.canyon.A06.com/api/auth/register
```
Apabila telah berhasil akan muncul tampilan sebagai berikut : 

![17apacheregis-awal](https://github.com/yusnaaaaa/Jarkom-Modul-3-A06-2023/assets/114417418/e6c212b2-2599-41cd-bc1e-b31c844f602e)

![17apcregis-awal](https://github.com/yusnaaaaa/Jarkom-Modul-3-A06-2023/assets/114417418/d6f7bce2-6776-4bbf-a1fa-13efb2813e01)


## Soal 16
b. POST /auth/login

### Penyelesaian soal 16

Untuk melakukan testing, jalankan command dengan menggunakan curl pada client sebagai berikut : 
```
curl -X POST -d '{"username": "username", "password": "password"}' -H "Content-Type: application/json" http://riegel.canyon.A06.com/api/auth/login
```
Ketika telah berhasil akan muncul tampilan sebagai berikut : 

![16curl](https://github.com/yusnaaaaa/Jarkom-Modul-3-A06-2023/assets/114417418/01fe3590-e53d-4d68-bf27-272d459d4464)

Setelah itu jalankan dengan Apache benchmark seperti dibawah ini : 
```
ab -n 100 -c 10 -p <(curl -X POST -d '{"username": "username", "password": "password"}' -H "Content-Type: application/json" http://riegel.canyon.A06.com/api/auth/login
) -T "application/json" http://riegel.canyon.A06.com/api/auth/login
```
Apabila telah berhasil akan muncul tampilan sebagai berikut : 

![17apachelogin-awal](https://github.com/yusnaaaaa/Jarkom-Modul-3-A06-2023/assets/114417418/816f69e4-c75e-4918-970a-6cf5a413ad76)

![17apclogin-akhir](https://github.com/yusnaaaaa/Jarkom-Modul-3-A06-2023/assets/114417418/cbf32e65-7f88-471a-9497-a20b6b18c6c7)

## Soal 17
c. GET /me

### Penyelesaian soal 17
```
curl -H "Authorization: Bearer [token]" http://riegel.canyon.A06.com/api/me
```

Ketika telah berhasil akan muncul tampilan sebagai berikut : 

![17curl](https://github.com/yusnaaaaa/Jarkom-Modul-3-A06-2023/assets/91377793/3f6fa0e6-2cde-4308-b675-096ca4d3da4a)

Setelah itu jalankan dengan Apache benchmark seperti dibawah ini :
```
ab -n 100 -c 10 -p <(curl -H "Authorization: Bearer [token]" http://riegel.canyon.A06.com/api/me
) -T "application/json" http://riegel.canyon.A06.com/api/me
```
Apabila telah berhasil akan muncul tampilan sebagai berikut : 

![17apcautho-awal](https://github.com/yusnaaaaa/Jarkom-Modul-3-A06-2023/assets/91377793/6d8509b6-0b6b-4089-a77b-27babba36c12) </br>

![17apcautho-akhir](https://github.com/yusnaaaaa/Jarkom-Modul-3-A06-2023/assets/91377793/60ada0c9-9267-4b45-8990-36d85f3ebec1)

## Soal 18
Untuk memastikan ketiganya bekerja sama secara adil untuk mengatur Riegel Channel maka implementasikan Proxy Bind pada Eisen untuk mengaitkan IP dari Frieren, Flamme, dan Fern.

### Penyelesaian soal 18
Untuk menyelesaikan soal ini menggunakan Proxy Bind pada Eisen (Load Balancer) untuk menghubungkan IP Worker Laravel dengan IP Load Balancer, maka akan ditambahkan script seperti dibawah ini : 
```
 location /frieren {
        proxy_bind 10.2.2.3;	
        proxy_pass http://10.2.4.1/index.php;
 
    }

    location /flamme {
	proxy_bind 10.2.2.3;
        proxy_pass http://10.2.4.2/index.php;
       
    }

    location /fern {
	proxy_bind 10.2.2.3;
        proxy_pass http://10.2.4.3/index.php;
	}
```
Kemudian lakukan `service nginx restart`
Setelah itu kita dapat melakukan testing pada client dengan command `lynx http://[ip lb]/[nama node worker laravel]/`, maka akan muncul tampilan hasil seperti dibawah ini : </br>
![18](https://github.com/yusnaaaaa/Jarkom-Modul-3-A06-2023/assets/91377793/8f96cbda-6bf3-46c8-abe2-1035d6ec81ed)

## Soal 19
Untuk meningkatkan performa dari Worker, coba implementasikan PHP-FPM pada Frieren, Flamme, dan Fern. Untuk testing kinerja naikkan 
- pm.max_children
- pm.start_servers
- pm.min_spare_servers
- pm.max_spare_servers
sebanyak tiga percobaan dan lakukan testing sebanyak 100 request dengan 10 request/second kemudian berikan hasil analisisnya pada Grimoire.

### Penyelesaian soal 19
Konfigurasi PHP-FPM untuk mengelola pekerja PHP pada setiap worker melibatkan beberapa parameter utama:

pm.max_children: Menentukan jumlah maksimum pekerja PHP yang dapat berjalan bersamaan. Harus disesuaikan dengan kapasitas sumber daya server agar tidak terlalu rendah atau tinggi, menghindari kelebihan beban atau kekurangan sumber daya.
pm.start_servers: Menentukan jumlah pekerja PHP yang akan dimulai otomatis ketika PHP-FPM pertama kali dijalankan atau direstart. Berguna untuk mengoptimalkan performa pada saat server pertama kali dimulai.
pm.min_spare_servers: Menentukan jumlah minimum pekerja PHP yang tetap berjalan saat server berjalan. Mempertahankan responsivitas server bahkan saat lalu lintas rendah.
pm.max_spare_servers: Menentukan jumlah maksimum pekerja PHP yang berjalan tetapi tidak menangani permintaan. Disesuaikan dengan kebutuhan untuk menangani lonjakan lalu lintas tanpa menambahkan terlalu banyak sumber daya saat beban rendah.

Pertama yaitu jalankan command pada worker Laravel seperti dibawah ini : 
```
echo ‘
user = eisen_user
group = eisen_user
listen = /var/run/php8.0-fpm-eisen-site.sock
listen.owner = www-data
listen.group = www-data
php_admin_value[disable_functions] = exec,passthru,shell_exec,system
php_admin_flag[allow_url_fopen] = off

pm = dynamic
pm.max_children = 75
pm.start_servers = 10
pm.min_spare_servers = 5
pm.max_spare_servers = 20
pm.process_idle_timeout = 10s
’ > /etc/php/8.0/fpm/pool.d/eisen.conf

groupadd eisen_user
useradd -g eisen_user eisen_user
```

Kemudian ubah beberapa konfigurasi socker php-fpm sebagai berikut : 
```
location ~ \.php$ {
                include snippets/fastcgi-php.conf;
        #
        #       # With php-fpm (or other unix sockets):
                fastcgi_pass unix:/var/run/php8.0-fpm-eisen-site.sock;
        #       # With php-cgi (or other tcp sockets):
        #       fastcgi_pass 127.0.0.1:9000;
}
```

Lalu, jalankan command dibawah ini : 
```
service php8.0-fpm start
service nginx restart
```

Setelah itu kita dapat melakukan testing dengan 3 konfigurasi yang berbeda sesuai dengan yang diperintahkan. Maka, ada 3 hasil sebagai berikut : 
- Hasil 1
```
pm = dynamic
pm.max_children = 75
pm.start_servers = 10
pm.min_spare_servers = 5
pm.max_spare_servers = 20
pm.process_idle_timeout = 10s
```
![19hasil1-awal](https://github.com/yusnaaaaa/Jarkom-Modul-3-A06-2023/assets/91377793/ab390338-b8cc-4af6-866f-ebc3834dc13b) </br>

![19hasil1-akhir](https://github.com/yusnaaaaa/Jarkom-Modul-3-A06-2023/assets/91377793/4852f912-03e1-4968-ba68-449a6421ef4d) </br>

- Hasil 2
```
pm = dynamic
pm.max_children = 35
pm.start_servers = 5
pm.min_spare_servers = 1
pm.max_spare_servers = 5
pm.process_idle_timeout = 6s
```
![19hasil2-awal](https://github.com/yusnaaaaa/Jarkom-Modul-3-A06-2023/assets/91377793/7f0e5be3-e3d1-47b8-844f-f6f6eb4a65d7) </br>

![19hasil2-akhir](https://github.com/yusnaaaaa/Jarkom-Modul-3-A06-2023/assets/91377793/c8b4e911-a714-4bb5-b7cd-722a08449842) </br>

- Hasil 3
```
pm = dynamic
pm.max_children = 45
pm.start_servers = 2
pm.min_spare_servers = 3
pm.max_spare_servers = 15
pm.process_idle_timeout = 8s
```
![19hasil3-awal](https://github.com/yusnaaaaa/Jarkom-Modul-3-A06-2023/assets/91377793/5b194bfe-a9bb-43b1-a53f-49f59668397e)</br>

![19hasil3-akhir](https://github.com/yusnaaaaa/Jarkom-Modul-3-A06-2023/assets/91377793/b69d6b0a-a161-470f-8754-4f60c2a06e6a) </br>

## Soal 20
Nampaknya hanya menggunakan PHP-FPM tidak cukup untuk meningkatkan performa dari worker maka implementasikan Least-Conn pada Eisen. Untuk testing kinerja dari worker tersebut dilakukan sebanyak 100 request dengan 10 request/second.

### Penyelesaian soal 20
Pertama yaitu kita harus mengubah konfigurasi pada node Eisen (Load Balancer) sebagai berikut : 
```
upstream laravel {
    least_conn;
    server 10.2.4.1;
    server 10.2.4.2;
    server 10.2.4.3;
}
```
Setelah berhasil maka akan muncul tampilan seperti dibawah ini : 

![20awal](https://github.com/yusnaaaaa/Jarkom-Modul-3-A06-2023/assets/91377793/0ac598c7-16e3-43ef-8361-428a4a085afc) </br>

![20akhir](https://github.com/yusnaaaaa/Jarkom-Modul-3-A06-2023/assets/91377793/5dd177a6-48be-4bc7-8ab4-59c332b0d400) </br>

