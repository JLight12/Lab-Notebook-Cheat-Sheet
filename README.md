# ECT/ITS Lab Notebook Cheatsheet

### VyOS Config

##### Full VyOS 1.2x Guide - it is really good and not too long.

> https://docs.vyos.io/en/crux

Switch into configuration mode.
```
config
```

Show Current Configuration
```
show
```

Push the configuration to the interfaces
```
commit
```

Configure Interfaces
```
set interfaces ethernet eth1 address 132.235.160.X/28
```

Default Route - This only needs to be done **once per router.**
```
set protocols static route 0.0.0.0/0 next-hop 132.235.160.254
```

Static Route Update
```
set protocols static route 100.70.111.64/26 next-hop 100.70.111.241
```

DNS Servers
````
set system name-server 132.235.9.75
set system name-server 132.235.200.41
````

DHCP Server
````
set service dhcp-server shared-network-name SUB1_POOL subnet 192.168.12.0/24 range 0 start 192.168.12.1
set service dhcp-server shared-network-name SUB1_POOL subnet 192.168.12.0/24 range 0 stop 192.168.12.50
set service dhcp-server shared-network-name SUB1_POOL subnet 192.168.12.0/24 default-router 192.168.12.254
set service dhcp-server shared-network-name SUB1_POOL subnet 192.168.12.0/24 dns-server 132.235.9.75
set service dhcp-server shared-network-name SUB1_POOL subnet 192.168.12.0/24 dns-server 132.235.200.41
set service dhcp-server shared-network-name SUB1_POOL subnet 192.168.12.0/24 lease 120
````

Set NAT
````
set nat source rule 100 outbound-interface eth0

set nat source rule 100 source address 172.X.Y.Z/S

set nat source rule 100 translation address masquerade
````

VyOS VLAN Interfaces
````
set interfaces ethernet eth0 vif 310 address 132.235.160.1/28
set interfaces ethernet eth0 vif 100X address 192.168.11.254/24
````

IPv6 Config Interface
```
set interfaces ethernet eth1 address 2610:a8:4831:3XY::1/64
```

IPv6 Static Routing
```
set protocols static route6 ::/0 next-hop 2610:a8:4831:3XY::1
```

Show IPv6 Route table
```
show ipv6 route
```

Config Name Server
```
set system name-server 2610:a8:4831:310::1
```

Config Host-Name
````
set system host-name ###
````

Configure IPv6 RA
````
set interfaces ethernet eth1 ipv6 router-advert prefix 2610:a8:4831:3XY::/64
set interfaces ethernet eth1 ipv6 router-advert name-server 2610:a8:4831:310::1
````

Advanced Config Commands
```
show system | commands
```

Ubuntu-CLI
````
sudo nmcli general hostname <PICK A HOSTNAME>
sudo nmcli con mod "Wired connection 1" ipv4.addresses 100.70.KKK.Y/26
sudo nmcli con mod "Wired connection 1" ipv4.gateway 100.70.KKK.Q
sudo nmcli con mod "Wired connection 1" ipv4.dns 132.235.9.75
sudo nmcli con mod "Wired connection 1" ipv4.method manual
sudo nmcli connection down "Wired connection 1"
sudo nmcli connection up "Wired connection 1"
````

SSH
````
ssh itsclass@X.X.X.X
````

Useful Commands
````
(U)Traceroute6: traceroute6 -n #####
(U)Ping6: ping6 #####
(W)tracert -6 -d #####
(W)ping -6 #####
````

## **IPv4 Quick Subnetting Table** ## 
|     |               |      |
|-----|---------------|------|
| /22 | 255.255.252.0 | 1024 |
| /23 | 255.255.254.0 | 512 |
|**/24**| **255.255.255.0**| **256** |
| /25 | 255.255.255.128 | 128 |
| /26 | 255.255.255.192 | 64 |
| /27 | 255.255.255.224 | 32 |
| /28 | 255.255.255.240 | 16 |
| /29 | 255.255.255.248 | 8 |
| /30 | 255.255.255.252 | 4 |
| /31 | 255.255.255.254 | 2 |
| /32 | 255.255.255.255 | 1 |
