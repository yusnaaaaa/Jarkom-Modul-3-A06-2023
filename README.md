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



## Soal 1

### Penyelesaian soal 1

## Soal 2

### Penyelesaian soal 2

## Soal 3

### Penyelesaian soal 3

## Soal 4

### Penyelesaian soal 4

## Soal 5

### Penyelesaian soal 5

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
