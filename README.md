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
- Frieren
```
auto eth0
iface eth0 inet dhcp
hwaddress ether 7a:6d:c7:77:9b:fb
```
- Flamme
```
auto eth0
iface eth0 inet dhcp
hwaddress ether 3e:26:cc:9e:a3:1e
```
- Fern
```
auto eth0
iface eth0 inet dhcp
hwaddress ether 82:69:33:8f:d8:e1
```

#### PHP Worker
- Lawine
```
auto eth0
iface eth0 inet dhcp
hwaddress ether 02:0f:9c:37:c7:60
```
- Linie
```
auto eth0
iface eth0 inet dhcp
hwaddress ether aa:f6:88:e0:1c:73
```
- Lugner
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

### Penyelesaian soal 7

## Soal 8

### Penyelesaian soal 8

## Soal 9

### Penyelesaian soal 9

## Soal 10

### Penyelesaian soal 10

## Soal 11

### Penyelesaian soal 11

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
