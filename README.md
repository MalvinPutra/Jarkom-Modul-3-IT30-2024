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
