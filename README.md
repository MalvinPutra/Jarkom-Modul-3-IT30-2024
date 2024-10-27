# Jarkom-Modul-3-IT30-2024

| Nama | NRP |
|---------------------------|------------|
|Riskiyatul Nur Oktarani | 5027231013 |
|Malvin Putra Rismahardian | 5027231048 |

<hr>

### Topologi IT30

![WhatsApp Image 2024-10-27 at 20 29 41_5239e940](https://github.com/user-attachments/assets/a3c7f5e4-36c1-44ed-91d7-9ed17bf97597)


### configuration

**ip prefix**
```
192.248
```

**Paradis(router)**

```
auto eth0
iface eth0 inet dhcp

auto eth1
iface eth1 inet static
	address 192.248.1.1
	netmask 255.255.255.0

auto eth2
iface eth2 inet static
	address 192.248.2.1
	netmask 255.255.255.0

auto eth3
iface eth3 inet static
	address 192.248.3.1
	netmask 255.255.255.0

auto eth4
iface eth4 inet static
	address 192.248.4.1
	netmask 255.255.255.0
```

**Armin**

```
auto eth0
iface eth0 inet static
	address 192.248.2.2
	netmask 255.255.255.0
	gateway 192.248.2.1
```

**Eren**
```
auto eth0
iface eth0 inet static
	address 192.248.2.3
	netmask 255.255.255.0
	gateway 192.248.2.1
```

**Mikasa**
```
auto eth0
iface eth0 inet static
	address 192.248.2.4
	netmask 255.255.255.0
	gateway 192.248.2.1
```

**Fritzs**
```
auto eth0
iface eth0 inet static
	address 192.248.4.2
	netmask 255.255.255.0
	gateway 192.248.4.1
```

**Annie**
```
auto eth0
iface eth0 inet static
	address 192.248.1.2
	netmask 255.255.255.0
	gateway 192.248.1.1
```

**Bertholdt**
```
auto eth0
iface eth0 inet static
	address 192.248.1.3
	netmask 255.255.255.0
	gateway 192.248.1.1
```

**Reiner**
```
auto eth0
iface eth0 inet static
	address 192.248.1.4
	netmask 255.255.255.0
	gateway 192.248.1.1
```

**Beast**
```
auto eth0
iface eth0 inet static
	address 192.248.3.2
	netmask 255.255.255.0
	gateway 192.248.3.1
```

**Colossal**
```
auto eth0
iface eth0 inet static
	address 192.248.3.3
	netmask 255.255.255.0
	gateway 192.248.3.1
```

**Warhammer**
```
auto eth0
iface eth0 inet static
	address 192.248.3.4
	netmask 255.255.255.0
	gateway 192.248.3.1
```

**Tybur**
```
auto eth0
iface eth0 inet static
	address 192.248.4.3
	netmask 255.255.255.0
	gateway 192.248.4.1
```

## Setup Node

**Fritz (DNS Server)**
```
echo 'nameserver 192.168.122.1' > /etc/resolv.conf
apt-get update
apt-get install bind9 -y

echo 'options {
        directory "/var/cache/bind";

        forwarders {
                192.168.122.1;
        };

        // dnssec-validation auto;
        allow-query{any;};
        auth-nxdomain no;
        listen-on-v6 { any; };
}; ' >/etc/bind/named.conf.options

service bind9 restart
```

**Soal 0 & 1**

Pulau Paradis telah menjadi tempat yang damai selama 1000 tahun, namun kedamaian tersebut tidak bertahan selamanya. Perang antara kaum Marley dan Eldia telah mencapai puncak. Kaum Marley yang dipimpin oleh Zeke, me-register domain name marley.yyy.com untuk worker Laravel mengarah pada Annie. Namun ternyata tidak hanya kaum Marley saja yang berinisiasi, kaum Eldia ternyata sudah mendaftarkan domain name eldia.yyy.com untuk worker PHP (0) mengarah pada Armin. (1)Lakukan konfigurasi sesuai dengan peta yang sudah diberikan.

*Silakan jalankan skrip berikut di Fritz untuk menambahkan domain eldia.it30.com.*

```bash
echo 'zone "marley.it30.com" { 
        type master; 
        file "/etc/bind/marley/marley.it30.com";
};

zone "eldia.it30.com" {
        type master;
        file "/etc/bind/eldia/eldia.it30.com";
}; ' >> /etc/bind/named.conf.local

mkdir /etc/bind/marley
mkdir /etc/bind/eldia

echo ';
; BIND data file for local loopback interface
;
$TTL    604800
@       IN      SOA     marley.it30.com. root.marley.it30.com. (
                              2         ; Serial
                         604800         ; Refresh
                          86400         ; Retry
                        2419200         ; Expire
                         604800 )       ; Negative Cache TTL
;
@       IN      NS      marley.it30.com.
@       IN      A       192.248.1.2     ; IP Annie' > /etc/bind/marley/marley.it30.com

echo ';
; BIND data file for local loopback interface
;
$TTL    604800
@       IN      SOA     eldia.it30.com. root.eldia.it30.com. (
                              2         ; Serial
                         604800         ; Refresh
                          86400         ; Retry
                        2419200         ; Expire
                         604800 )       ; Negative Cache TTL
;
@       IN      NS      eldia.it30.com.
@       IN      A       192.248.2.2     ; IP Armin' > /etc/bind/eldia/eldia.it30.com

service bind9 restart
```
