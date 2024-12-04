# Jarkom-Modul-5-IT44-2024

![Screenshot 2024-12-01 200158](https://github.com/user-attachments/assets/e6f29bc0-fa2d-47c0-99df-4aada13c47eb)

### Tabel pembagian ip dan routing
https://docs.google.com/spreadsheets/d/15IOt12VpeqdX2up8EsDzQyxtjz6CnoYE-tO2SPuVl_w/edit?usp=sharing


## Konfigurasi
### NewEridu
```
#NAT
auto eth0
iface eth0 inet dhcp

#A1
auto eth1
iface eth1 inet static
	address 10.85.2.217
	netmask 255.255.255.252

#A5
auto eth2
iface eth2 inet static
	address 10.85.2.221
	netmask 255.255.255.252

#ROUTING
#A2
route add -net 10.85.2.192 netmask 255.255.255.248 gw 10.85.2.218

#A3
route add -net 10.85.2.0 netmask 255.255.255.128 gw 10.85.2.218

#A4
route add -net 10.85.1.0 netmask 255.255.255.0 gw 10.85.2.218

#A6
route add -net 10.85.2.200 netmask 255.255.255.248 gw 10.85.2.222

#A7
route add -net 10.85.2.224 netmask 255.255.255.252 gw 10.85.2.222

#A8
route add -net 10.85.2.128 netmask 255.255.255.192 gw 10.85.2.222

#A9
route add -net 10.85.2.208 netmask 255.255.255.248 gw 10.85.2.222

#Otomasi iptables awal
IP_ETH0=$(ip -4 addr show eth0 | grep -oP '(?<=inet\s)\d+(\.\d+){3}')
iptables -t nat -A POSTROUTING -o eth0 -j SNAT --to-source $IP_ETH0
```

### LuminaSquare
```
#A1
auto eth0
iface eth0 inet static
	address 10.85.2.218
	netmask 255.255.255.252
    gateway 10.67.2.217

#A2
auto eth1
iface eth1 inet static
	address 10.85.2.193
	netmask 255.255.255.248

#A4
auto eth2
iface eth2 inet static
	address 10.85.1.1
	netmask 255.255.255.0

#ROUTING
#A3
route add -net 10.85.2.0 netmask 255.255.255.128 gw 10.85.2.195

#A7
route add -net 10.85.2.224 netmask 255.255.255.252 gw 10.85.2.217

#A8
route add -net 10.85.2.128 netmask 255.255.255.192 gw 10.85.2.217

#A9
route add -net 10.85.2.208 netmask 255.255.255.248 gw 10.85.2.217

echo 'nameserver 192.168.122.1' > /etc/resolv.conf
apt-get update
apt install isc-dhcp-relay -y

echo 'SERVERS="10.85.2.211"
INTERFACES="eth0 eth1 eth2 eth3"
OPTIONS=""
' > /etc/default/isc-dhcp-relay

echo 'net.ipv4.ip_forward=1' >> /etc/sysctl.conf

service isc-dhcp-relay restart
```

### BalletTwins
```
#A2
auto eth0
iface eth0 inet static
	address 10.85.2.195
	netmask 255.255.255.248
    gateway 10.85.2.193

#A3
auto eth1
iface eth1 inet static
	address 10.85.2.1
	netmask 255.255.255.128

#ROUTING
#A4
route add -net 10.85.1.0 netmask 255.255.255.0 gw 10.85.2.193

#A7
route add -net 10.85.2.224 netmask 255.255.255.252 gw 10.85.2.193

#A8
route add -net 10.85.2.128 netmask 255.255.255.192 gw 10.85.2.193

#A9
route add -net 10.85.2.208 netmask 255.255.255.248 gw 10.85.2.193

echo 'nameserver 192.168.122.1' > /etc/resolv.conf
apt-get update
apt install isc-dhcp-relay -y

echo 'SERVERS="10.85.2.211"
INTERFACES="eth0 eth1 eth2 eth3"
OPTIONS=""
' > /etc/default/isc-dhcp-relay

echo 'net.ipv4.ip_forward=1' >> /etc/sysctl.conf

service isc-dhcp-relay restart
```

### SixStreet
```
#A5
auto eth0
iface eth0 inet static
	address 10.85.2.222
	netmask 255.255.255.252
    gateway 10.85.2.221

#A6
auto eth2
iface eth2 inet static
	address 10.85.2.201
	netmask 255.255.255.248

#A9
auto eth1
iface eth1 inet static
	address 10.85.2.209
	netmask 255.255.255.248

#ROUTING
#A2
route add -net 10.85.2.192 netmask 255.255.255.248 gw 10.85.2.221

#A3
route add -net 10.85.2.0 netmask 255.255.255.128 gw 10.85.2.221

#A4
route add -net 10.85.1.0 netmask 255.255.255.0 gw 10.85.2.221

#A7
route add -net 10.85.2.224 netmask 255.255.255.252 gw 10.85.2.203

#A8
route add -net 10.85.2.128 netmask 255.255.255.192 gw 10.85.2.202

echo 'nameserver 192.168.122.1' > /etc/resolv.conf
apt-get update
apt install isc-dhcp-relay -y

echo 'SERVERS="10.85.2.211"
INTERFACES="eth0 eth1 eth2 eth3"
OPTIONS=""
' > /etc/default/isc-dhcp-relay

echo 'net.ipv4.ip_forward=1' >> /etc/sysctl.conf

service isc-dhcp-relay restart
```

### OuterRing
```
#A6
auto eth0
iface eth0 inet static
	address 10.85.2.202
	netmask 255.255.255.248
    gateway 10.85.2.201

#A8
auto eth1
iface eth1 inet static
	address 10.85.2.129
	netmask 255.255.255.192

#ROUTING
#A2
route add -net 10.85.2.192 netmask 255.255.255.248 gw 10.85.2.201

#A3
route add -net 10.85.2.0 netmask 255.255.255.128 gw 10.85.2.201

#A4
route add -net 10.85.1.0 netmask 255.255.255.0 gw 10.85.2.201

#A7
route add -net 10.85.2.224 netmask 255.255.255.252 gw 10.85.2.203

#A9
route add -net 10.85.2.208 netmask 255.255.255.248 gw 10.85.2.201

echo 'nameserver 192.168.122.1' > /etc/resolv.conf
apt-get update
apt install isc-dhcp-relay -y

echo 'SERVERS="10.85.2.211"
INTERFACES="eth0 eth1 eth2 eth3"
OPTIONS=""
' > /etc/default/isc-dhcp-relay

echo 'net.ipv4.ip_forward=1' >> /etc/sysctl.conf

service isc-dhcp-relay restart
```

### ScootOutpost
```
#A6
auto eth0
iface eth0 inet static
	address 10.85.2.203
	netmask 255.255.255.248
    gateway 10.85.2.201

#A7
auto eth1
iface eth1 inet static
	address 10.85.2.225
	netmask 255.255.255.252

#ROUTING
#A2
route add -net 10.85.2.192 netmask 255.255.255.248 gw 10.85.2.201

#A3
route add -net 10.85.2.0 netmask 255.255.255.128 gw 10.85.2.201

#A4
route add -net 10.85.1.0 netmask 255.255.255.0 gw 10.85.2.201

#A8
route add -net 10.85.2.128 netmask 255.255.255.192 gw 10.85.2.202

#A9
route add -net 10.85.2.208 netmask 255.255.255.248 gw 10.85.2.201

echo 'nameserver 192.168.122.1' > /etc/resolv.conf
```
### HollowZero
```
auto eth0
iface eth0 inet static
	address 10.85.2.226
	netmask 255.255.255.252
    gateway 10.85.2.225

#ROUTING
echo 'nameserver 192.168.122.1' > /etc/resolv.conf
apt-get update
apt-get install apache2 netcat -y

service apache2 start

echo 'Welcome to {hostname}' > /var/www/html/index.html

service apache2 restart
```

### Fairy
```
auto eth0
iface eth0 inet static
	address 10.85.2.211
	netmask 255.255.255.248
    gateway 10.85.2.209

#ROUTING
echo 'nameserver 192.168.122.1' > /etc/resolv.conf
apt-get update
apt-get install isc-dhcp-server netcat -y

echo 'INTERFACESv4="eth0"' > /etc/default/isc-dhcp-server

echo '#A8
subnet 10.85.2.128 netmask 255.255.255.192 {
        range 10.85.2.130 10.85.2.190;
        option routers 10.85.2.129; # Gateway
        option broadcast-address 10.85.2.191;
        option domain-name-servers 10.85.2.210; #IP HDD
        default-lease-time 600;
        max-lease-time 7200;
}

#A4
subnet 10.85.1.0 netmask 255.255.255.0 {
        range 10.85.1.2 10.85.1.254;
        option routers 10.85.1.1;
        option broadcast-address 10.85.1.255;
        option domain-name-servers 10.85.2.210;
        default-lease-time 600;
        max-lease-time 7200;
}

#A3
subnet 10.85.2.0 netmask 255.255.255.128 {
        range 10.85.2.2 10.85.2.126;
        option routers 10.85.2.1;
        option broadcast-address 10.85.2.127;
        option domain-name-servers 10.85.2.210;
        default-lease-time 600;
        max-lease-time 7200;
}

subnet 10.85.2.216 netmask 255.255.255.252 {}
subnet 10.85.2.192 netmask 255.255.255.248 {}
subnet 10.85.2.220 netmask 255.255.255.252 {}
subnet 10.85.2.200 netmask 255.255.255.248 {}
subnet 10.85.2.224 netmask 255.255.255.252 {}
subnet 10.85.2.208 netmask 255.255.255.248 {}
' > /etc/dhcp/dhcpd.conf

service isc-dhcp-server restart
```

### HDD
```
auto eth0
iface eth0 inet static
	address 10.85.2.210
	netmask 255.255.255.248
    gateway 10.85.2.209

#ROUTING
echo 'nameserver 192.168.122.1' > /etc/resolv.conf
apt-get update
apt-get install bind9 netcat -y

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
### HIA
```
auto eth0
iface eth0 inet static
	address 10.85.2.194
	netmask 255.255.255.248
    gateway 10.85.2.193

#ROUTING
echo 'nameserver 192.168.122.1' > /etc/resolv.conf
apt-get update
apt-get install apache2 netcat -y

service apache2 start

echo 'Welcome to {hostname}' > /var/www/html/index.html

service apache2 restart
```
### Caesar, Burnice, 
```
auto eth0
iface eth0 inet dhcp
```
