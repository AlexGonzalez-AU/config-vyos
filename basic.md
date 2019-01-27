# vyos

## Create the VM
* Gen 1
* 1 vCPU 
* 512MB RAM
* 16GB Disk 
* 4 NICs 

Boot the 8.1.1-amd64.iso and login: vyos, vyos.

## Install

``` vyos
$ install image (yes; auto; sda; yes; <max>; 1.1.8; /config/config.boot; <password>; sda)
```

## Enable SSH

``` vyos
$ configure
# set interfaces ethernet eth0 address 10.10.0.1/24
# set service ssh port 22
# set service ssh listen-address 10.10.0.1
# set service ssh listen-address 10.11.0.1
# set service ssh listen-address 10.12.0.1
# commit
# save
```

It is now possible to use the new native ssh client form Windows 10 to connect.

``` powershell
PS > ssh vyos@10.20.0.1
```

## Configure

### Interfaces

``` vyos
# set interfaces ethernet eth0 address 10.10.0.1/24
# set interfaces ethernet eth1 address 10.11.0.1/24
# set interfaces ethernet eth2 address 10.12.0.1/24
# set interfaces ethernet eth3 address dhcp
```

### DHCP

> n.b. the `start` and `stop` commands will change slightly in versions of vyos greater than v1.9.9. 

``` vyos
$ configure
# set service dhcp-server shared-network-name 10 subnet 10.10.0.0/24 default-router 10.10.0.1
# set service dhcp-server shared-network-name 10 subnet 10.10.0.0/24 dns-server 8.8.8.8
# set service dhcp-server shared-network-name 10 subnet 10.10.0.0/24 start 10.10.0.100 stop 10.10.0.199

# set service dhcp-server shared-network-name 11 subnet 10.11.0.0/24 default-router 10.11.0.1
# set service dhcp-server shared-network-name 11 subnet 10.11.0.0/24 dns-server 8.8.8.8
# set service dhcp-server shared-network-name 11 subnet 10.11.0.0/24 start 10.11.0.100 stop 10.11.0.199

# set service dhcp-server shared-network-name 12 subnet 10.12.0.0/24 default-router 10.12.0.1
# set service dhcp-server shared-network-name 12 subnet 10.12.0.0/24 dns-server 8.8.8.8
# set service dhcp-server shared-network-name 12 subnet 10.12.0.0/24 start 10.12.0.100 stop 10.12.0.199
# commit
# save
```

### NAT

``` vyos
$ configure
# set nat source rule 100 outbound-interface eth3
# set nat source rule 100 translation address masquerade
# commit
# save
```

### Firewall

``` vyos
$ configure 
# set firewall group network-group MICROSOFT network 13.64.0.0/11
# set firewall group network-group MICROSOFT network 13.96.0.0/13
# set firewall group network-group MICROSOFT network 13.104.0.0/14
# set firewall group network-group MICROSOFT network 20.36.0.0/14
# set firewall group network-group MICROSOFT network 20.40.0.0/13
# set firewall group network-group MICROSOFT network 20.128.0.0/16
# set firewall group network-group MICROSOFT network 20.140.0.0/15
# set firewall group network-group MICROSOFT network 20.144.0.0/14
# set firewall group network-group MICROSOFT network 20.160.0.0/12
# set firewall group network-group MICROSOFT network 20.176.0.0/14
# set firewall group network-group MICROSOFT network 20.180.0.0/14
# set firewall group network-group MICROSOFT network 20.184.0.0/13
# set firewall group network-group MICROSOFT network 23.96.0.0/13
# set firewall group network-group MICROSOFT network 40.64.0.0/10
# set firewall group network-group MICROSOFT network 42.159.0.0/16
# set firewall group network-group MICROSOFT network 51.4.0.0/15
# set firewall group network-group MICROSOFT network 51.8.0.0/16
# set firewall group network-group MICROSOFT network 51.10.0.0/15
# set firewall group network-group MICROSOFT network 51.12.0.0/15
# set firewall group network-group MICROSOFT network 51.18.0.0/16
# set firewall group network-group MICROSOFT network 51.51.0.0/16
# set firewall group network-group MICROSOFT network 51.53.0.0/16
# set firewall group network-group MICROSOFT network 51.103.0.0/16
# set firewall group network-group MICROSOFT network 51.104.0.0/15
# set firewall group network-group MICROSOFT network 51.107.0.0/16
# set firewall group network-group MICROSOFT network 51.116.0.0/16
# set firewall group network-group MICROSOFT network 51.120.0.0/16
# set firewall group network-group MICROSOFT network 51.124.0.0/16
# set firewall group network-group MICROSOFT network 51.132.0.0/16
# set firewall group network-group MICROSOFT network 51.136.0.0/15
# set firewall group network-group MICROSOFT network 51.138.0.0/16
# set firewall group network-group MICROSOFT network 51.140.0.0/14
# set firewall group network-group MICROSOFT network 51.144.0.0/15
# set firewall group network-group MICROSOFT network 52.96.0.0/12
# set firewall group network-group MICROSOFT network 52.112.0.0/14
# set firewall group network-group MICROSOFT network 52.120.0.0/14
# set firewall group network-group MICROSOFT network 52.125.0.0/16
# set firewall group network-group MICROSOFT network 52.126.0.0/15
# set firewall group network-group MICROSOFT network 52.130.0.0/15
# set firewall group network-group MICROSOFT network 52.132.0.0/14
# set firewall group network-group MICROSOFT network 52.136.0.0/13
# set firewall group network-group MICROSOFT network 52.145.0.0/16
# set firewall group network-group MICROSOFT network 52.146.0.0/15
# set firewall group network-group MICROSOFT network 52.148.0.0/14
# set firewall group network-group MICROSOFT network 52.152.0.0/13
# set firewall group network-group MICROSOFT network 52.160.0.0/11
# set firewall group network-group MICROSOFT network 52.224.0.0/11
# set firewall group network-group MICROSOFT network 64.4.0.0/18
# set firewall group network-group MICROSOFT network 65.52.0.0/14
# set firewall group network-group MICROSOFT network 66.119.144.0/20
# set firewall group network-group MICROSOFT network 70.37.0.0/17
# set firewall group network-group MICROSOFT network 70.37.128.0/18
# set firewall group network-group MICROSOFT network 91.190.216.0/21
# set firewall group network-group MICROSOFT network 94.245.64.0/18
# set firewall group network-group MICROSOFT network 103.9.8.0/22
# set firewall group network-group MICROSOFT network 103.25.156.0/24
# set firewall group network-group MICROSOFT network 103.25.157.0/24
# set firewall group network-group MICROSOFT network 103.25.158.0/23
# set firewall group network-group MICROSOFT network 103.36.96.0/22
# set firewall group network-group MICROSOFT network 103.255.140.0/22
# set firewall group network-group MICROSOFT network 104.40.0.0/13
# set firewall group network-group MICROSOFT network 104.146.0.0/15
# set firewall group network-group MICROSOFT network 104.208.0.0/13
# set firewall group network-group MICROSOFT network 111.221.16.0/20
# set firewall group network-group MICROSOFT network 111.221.64.0/18
# set firewall group network-group MICROSOFT network 129.75.0.0/16
# set firewall group network-group MICROSOFT network 131.253.1.0/24
# set firewall group network-group MICROSOFT network 131.253.3.0/24
# set firewall group network-group MICROSOFT network 131.253.5.0/24
# set firewall group network-group MICROSOFT network 131.253.6.0/24
# set firewall group network-group MICROSOFT network 131.253.8.0/24
# set firewall group network-group MICROSOFT network 131.253.12.0/22
# set firewall group network-group MICROSOFT network 131.253.16.0/23
# set firewall group network-group MICROSOFT network 131.253.18.0/24
# set firewall group network-group MICROSOFT network 131.253.21.0/24
# set firewall group network-group MICROSOFT network 131.253.22.0/23
# set firewall group network-group MICROSOFT network 131.253.24.0/21
# set firewall group network-group MICROSOFT network 131.253.32.0/20
# set firewall group network-group MICROSOFT network 131.253.61.0/24
# set firewall group network-group MICROSOFT network 131.253.62.0/23
# set firewall group network-group MICROSOFT network 131.253.64.0/18
# set firewall group network-group MICROSOFT network 131.253.128.0/17
# set firewall group network-group MICROSOFT network 132.245.0.0/16
# set firewall group network-group MICROSOFT network 134.170.0.0/16
# set firewall group network-group MICROSOFT network 134.177.0.0/16
# set firewall group network-group MICROSOFT network 137.116.0.0/15
# set firewall group network-group MICROSOFT network 137.135.0.0/16
# set firewall group network-group MICROSOFT network 138.91.0.0/16
# set firewall group network-group MICROSOFT network 138.196.0.0/16
# set firewall group network-group MICROSOFT network 139.217.0.0/16
# set firewall group network-group MICROSOFT network 139.219.0.0/16
# set firewall group network-group MICROSOFT network 141.251.0.0/16
# set firewall group network-group MICROSOFT network 146.147.0.0/16
# set firewall group network-group MICROSOFT network 147.243.0.0/16
# set firewall group network-group MICROSOFT network 150.171.0.0/16
# set firewall group network-group MICROSOFT network 150.242.48.0/22
# set firewall group network-group MICROSOFT network 157.54.0.0/15
# set firewall group network-group MICROSOFT network 157.56.0.0/14
# set firewall group network-group MICROSOFT network 157.60.0.0/16
# set firewall group network-group MICROSOFT network 167.220.0.0/16
# set firewall group network-group MICROSOFT network 168.61.0.0/16
# set firewall group network-group MICROSOFT network 168.62.0.0/15
# set firewall group network-group MICROSOFT network 191.232.0.0/13
# set firewall group network-group MICROSOFT network 192.32.0.0/16
# set firewall group network-group MICROSOFT network 192.48.225.0/24
# set firewall group network-group MICROSOFT network 192.84.159.0/24
# set firewall group network-group MICROSOFT network 192.84.160.0/23
# set firewall group network-group MICROSOFT network 192.100.102.0/24
# set firewall group network-group MICROSOFT network 192.100.103.0/24
# set firewall group network-group MICROSOFT network 192.197.157.0/24
# set firewall group network-group MICROSOFT network 193.149.64.0/19
# set firewall group network-group MICROSOFT network 193.221.113.0/24
# set firewall group network-group MICROSOFT network 194.69.96.0/19
# set firewall group network-group MICROSOFT network 194.110.197.0/24
# set firewall group network-group MICROSOFT network 198.105.232.0/22
# set firewall group network-group MICROSOFT network 198.200.130.0/24
# set firewall group network-group MICROSOFT network 198.206.164.0/24
# set firewall group network-group MICROSOFT network 199.60.28.0/24
# set firewall group network-group MICROSOFT network 199.74.210.0/24
# set firewall group network-group MICROSOFT network 199.103.90.0/23
# set firewall group network-group MICROSOFT network 199.103.122.0/24
# set firewall group network-group MICROSOFT network 199.242.32.0/20
# set firewall group network-group MICROSOFT network 199.242.48.0/21
# set firewall group network-group MICROSOFT network 202.89.224.0/20
# set firewall group network-group MICROSOFT network 204.13.120.0/21
# set firewall group network-group MICROSOFT network 204.14.180.0/22
# set firewall group network-group MICROSOFT network 204.79.135.0/24
# set firewall group network-group MICROSOFT network 204.79.179.0/24
# set firewall group network-group MICROSOFT network 204.79.181.0/24
# set firewall group network-group MICROSOFT network 204.79.188.0/24
# set firewall group network-group MICROSOFT network 204.79.195.0/24
# set firewall group network-group MICROSOFT network 204.79.196.0/23
# set firewall group network-group MICROSOFT network 204.79.252.0/24
# set firewall group network-group MICROSOFT network 204.152.18.0/23
# set firewall group network-group MICROSOFT network 204.152.140.0/23
# set firewall group network-group MICROSOFT network 204.231.192.0/24
# set firewall group network-group MICROSOFT network 204.231.194.0/23
# set firewall group network-group MICROSOFT network 204.231.197.0/24
# set firewall group network-group MICROSOFT network 204.231.198.0/23
# set firewall group network-group MICROSOFT network 204.231.200.0/21
# set firewall group network-group MICROSOFT network 204.231.208.0/20
# set firewall group network-group MICROSOFT network 204.231.236.0/24
# set firewall group network-group MICROSOFT network 205.174.224.0/20
# set firewall group network-group MICROSOFT network 206.138.168.0/21
# set firewall group network-group MICROSOFT network 206.191.224.0/19
# set firewall group network-group MICROSOFT network 207.46.0.0/16
# set firewall group network-group MICROSOFT network 207.68.128.0/18
# set firewall group network-group MICROSOFT network 208.68.136.0/21
# set firewall group network-group MICROSOFT network 208.76.44.0/22
# set firewall group network-group MICROSOFT network 208.84.0.0/21
# set firewall group network-group MICROSOFT network 209.240.192.0/19
# set firewall group network-group MICROSOFT network 213.199.128.0/18
# set firewall group network-group MICROSOFT network 216.32.180.0/22
# set firewall group network-group MICROSOFT network 216.220.208.0/20

# set firewall group network-group DNS network 8.8.8.8/32
# set firewall group network-group DNS network 8.8.4.4/32

# set firewall group port-group WEB port 80
# set firewall group port-group WEB port 443

# set firewall name 10NET-IN default-action drop
# set firewall name 11NET-IN default-action drop
# set firewall name 12NET-IN default-action drop
# set firewall name iNET-IN default-action drop
# set firewall name iNET-LOCAL default-action drop

# set interfaces ethernet eth0 firewall in name 10NET-IN 
# set interfaces ethernet eth1 firewall in name 11NET-IN
# set interfaces ethernet eth2 firewall in name 12NET-IN
# set interfaces ethernet eth3 firewall in name iNET-IN
# set interfaces ethernet eth3 firewall local name iNET-LOCAL

# set firewall name iNET-IN rule 100 action accept
# set firewall name iNET-IN rule 100 state established enable
# set firewall name iNET-IN rule 100 state related enable
# set firewall name iNET-IN rule 100 protocol udp
# set firewall name iNET-IN rule 100 source port 53
# set firewall name iNET-IN rule 100 source group network-group DNS

# set firewall name iNET-IN rule 200 action accept
# set firewall name iNET-IN rule 200 state established enable
# set firewall name iNET-IN rule 200 state related enable
# set firewall name iNET-IN rule 200 protocol tcp
# set firewall name iNET-IN rule 200 source group port-group WEB
## set firewall name iNET-IN rule 200 source group network-group MICROSOFT

# set firewall name iNET-IN rule 900 action drop
# set firewall name iNET-IN rule 900 state invalid enable

# set firewall name 10NET-IN rule 100 action accept
# set firewall name 10NET-IN rule 100 protocol udp
# set firewall name 10NET-IN rule 100 destination port 53
# set firewall name 10NET-IN rule 100 destination group network-group DNS

# set firewall name 10NET-IN rule 200 action accept
# set firewall name 10NET-IN rule 100 protocol tcp
# set firewall name 10NET-IN rule 200 destination group port-group WEB
## set firewall name 10NET-IN rule 200 destination group network-group MICROSOFT

# set firewall name 10NET-IN rule 900 action drop
# set firewall name 10NET-IN rule 900 state invalid enable

# commit
# save
```
