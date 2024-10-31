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

echo "zone \"marley.IT30.com\" {
	type master;
	file \"/etc/bind/jarkom/marley.IT30.com\";
};

zone \"eldia.IT30.com\" {
	type master;
	file \"/etc/bind/jarkom/eldia.IT30.com\";
};
" > /etc/bind/named.conf.local

mkdir /etc/bind/jarkom

marley="
;
;BIND data file for local loopback interface
;
\$TTL    604800
@    IN    SOA    marley.IT30.com. root.marley.IT30.com. (
        2        ; Serial
                604800        ; Refresh
                86400        ; Retry
                2419200        ; Expire
                604800 )    ; Negative Cache TTL
;                   
@    IN    NS    marley.IT32.com.
@       IN    A    192.248.1.2
"
echo "$marley" > /etc/bind/jarkom/marley.IT30.com

eldia="
;
;BIND data file for local loopback interface
;
\$TTL    604800
@    IN    SOA    eldia.IT30.com. root.eldia.IT30.com. (
        2        ; Serial
                604800        ; Refresh
                86400        ; Retry
                2419200        ; Expire
                604800 )    ; Negative Cache TTL
;                   
@    IN    NS    eldia.IT32.com.
@       IN    A    192.248.2.2
"
echo "$eldia" > /etc/bind/jarkom/eldia.IT30.com

service bind9 restart
```

**Soal 2 - 5**

Jauh sebelum perang dimulai, ternyata para keluarga bangsawan, Tybur dan Fritz, telah membuat kesepakatan sebagai berikut:

Semua Client harus menggunakan konfigurasi ip address dari keluarga Tybur (dhcp).

Client yang melalui bangsa marley mendapatkan range IP dari [prefix IP].1.05 - [prefix IP].1.25 dan [prefix IP].1.50 - [prefix IP].1.100 (2)

Client yang melalui bangsa eldia mendapatkan range IP dari [prefix IP].2.09 - [prefix IP].2.27 dan [prefix IP].2 .81 - [prefix IP].2.243 (3)

Client mendapatkan DNS dari keluarga Fritz dan dapat terhubung dengan internet melalui DNS tersebut (4)

Dikarenakan keluarga Tybur tidak menyukai kaum eldia, maka mereka hanya meminjamkan ip address ke kaum eldia selama 6 menit. Namun untuk kaum marley, keluarga Tybur meminjamkan ip address selama 30 menit. Waktu maksimal dialokasikan untuk peminjaman alamat IP selama 87 menit. (5)

pada Paradis (DHCP Relay) kita dapat membuat script bernama paradis.sh yang mengarah ke Tybur (DHCP Server)

###DHCP Relay (Paradis)

```

echo 'nameserver 192.168.122.1' > /etc/resolv.conf

apt-get update
apt-get install isc-dhcp-relay -y
service isc-dhcp-relay start

echo 'SERVERS="192.248.4.3"' > /etc/default/isc-dhcp-relay
echo 'INTERFACES="eth1 eth2 eth3 eth4"' >> /etc/default/isc-dhcp-relay
echo 'OPTIONS=""' >> /etc/default/isc-dhcp-relay

echo 'net.ipv4.ip_forward=1' > /etc/sysctl.conf

service isc-dhcp-relay restart

```

###DHCP Relay (Tybur)

```
echo 'nameserver 192.168.122.1' > /etc/resolv.conf

apt-get update
apt-get install isc-dhcp-server -y

echo 'INTERFACESv4="eth0"' > /etc/default/isc-dhcp-server
echo 'INTERFACESv6=""' >> /etc/default/isc-dhcp-server

echo 'option domain-name "example.org";' > /etc/dhcp/dhcpd.conf
echo 'option domain-name-servers ns1.example.org, ns2.example.org;' >> /etc/dhcp/dhcpd.conf
echo '' >> /etc/dhcp/dhcpd.conf
echo 'default-lease-time 600;' >> /etc/dhcp/dhcpd.conf
echo 'max-lease-time 7200;' >> /etc/dhcp/dhcpd.conf
echo '' >> /etc/dhcp/dhcpd.conf
echo 'ddns-update-style none;' >> /etc/dhcp/dhcpd.conf
echo '' >> /etc/dhcp/dhcpd.conf

echo 'subnet 192.248.1.0 netmask 255.255.255.0 {' >> /etc/dhcp/dhcpd.conf
echo '    range 192.248.1.5 192.248.1.25;' >> /etc/dhcp/dhcpd.conf
echo '    range 192.248.1.50 192.248.1.100;' >> /etc/dhcp/dhcpd.conf
echo '    option routers 192.248.1.1;' >> /etc/dhcp/dhcpd.conf
echo '    option broadcast-address 192.248.1.255;' >> /etc/dhcp/dhcpd.conf
echo '    option domain-name-servers 192.248.4.2;' >> /etc/dhcp/dhcpd.conf
echo '    default-lease-time 1800;' >> /etc/dhcp/dhcpd.conf
echo '    max-lease-time 5220;' >> /etc/dhcp/dhcpd.conf
echo '}' >> /etc/dhcp/dhcpd.conf
echo '' >> /etc/dhcp/dhcpd.conf

echo 'subnet 192.248.2.0 netmask 255.255.255.0 {' >> /etc/dhcp/dhcpd.conf
echo '    range 192.248.2.9 192.248.2.27;' >> /etc/dhcp/dhcpd.conf
echo '    range 192.248.2.81 192.248.2.243;' >> /etc/dhcp/dhcpd.conf
echo '    option routers 192.248.2.1;' >> /etc/dhcp/dhcpd.conf
echo '    option broadcast-address 192.248.2.255;' >> /etc/dhcp/dhcpd.conf
echo '    option domain-name-servers 192.248.4.2;' >> /etc/dhcp/dhcpd.conf
echo '    default-lease-time 360;' >> /etc/dhcp/dhcpd.conf
echo '    max-lease-time 5220;' >> /etc/dhcp/dhcpd.conf
echo '}' >> /etc/dhcp/dhcpd.conf
echo '' >> /etc/dhcp/dhcpd.conf

echo 'subnet 192.248.3.0 netmask 255.255.255.0 {' >> /etc/dhcp/dhcpd.conf
echo '}' >> /etc/dhcp/dhcpd.conf
echo '' >> /etc/dhcp/dhcpd.conf

echo 'subnet 192.248.4.0 netmask 255.255.255.0 {' >> /etc/dhcp/dhcpd.conf
echo '}' >> /etc/dhcp/dhcpd.conf

service isc-dhcp-server restart
```

**Output no 2**


**Output no 3**


**Output no 4**




**Soal no 6**

Armin berinisiasi untuk memerintahkan setiap worker PHP untuk melakukan konfigurasi virtual host untuk website berikut https://intip.in/BangsaEldia dengan menggunakan php 7.3 (6)

```
echo 'nameserver 192.248.4.2' > /etc/resolv.conf # IP DNS-SERVER

apt-get update

apt-get install nginx -y
apt-get install lynx -y
apt-get install php7.3 php7.3-fpm php7.3-mysql -y   # Install PHP 7.3 dan modul yang diperlukan
apt-get install wget -y
apt-get install unzip -y
apt-get install rsync -y    # Install rsync untuk transfer file

service nginx start
service php7.3-fpm start    # Jalankan PHP-FPM versi 7.3

wget --no-check-certificate 'https://drive.google.com/uc?export=download&id=1ufulgiWyTbOXQcow11JkXG7safgLq1y-' -O '/var/www/modul-3.zip'

unzip -o /var/www/modul-3.zip -d /var/www/
rm /var/www/modul-3.zip

rsync -av /var/www/modul-3/ /var/www/eldia.it30.com/

rm -r /var/www/modul-3

cp /etc/nginx/sites-available/default /etc/nginx/sites-available/eldia.it30.com

ln -s /etc/nginx/sites-available/eldia.it30.com /etc/nginx/sites-enabled/

rm /etc/nginx/sites-enabled/default

echo 'server {
    listen 80;
    server_name _;

    root /var/www/eldia.it30.com;
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
}' > /etc/nginx/sites-available/eldia.it30.com

service nginx restart
service php7.3-fpm restart
```
**output no 6**
