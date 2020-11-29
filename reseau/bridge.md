# Bridge

## Notions

### Virtuel

- peut-être vu comme un switch
- virtuel (pas de switch physique)
- utilise les adresses MAC
- link layers of OSI model
- redirige les trames d'une interface physique
- BPDU (Bridge Protocol Data Unit) échangés
- STP (Spanning Tree Protocol), niveau 2, algo -> topologie sans boucle


### Physique

- connecte les segments d'un reseau
- utilise une table pour envoyer les trames à travers le réseau
    - also called _forwarding database_
- algo : @mac non trouvée => broadcast sur tous les ports du bridge
    - filtering : destination node and host on the same side of the network segment
      the bridge blocks the frame from going to the other network segments.
    - forwarding : destination node and host are on different segments,
      then the bridge forward the received frame to the appropriate segment.
    - flooding : destination address in the frame received is unknown,
      then the bridge forward it to all the network segments except the source address.

## Cas pratique

### infos

```bash
uname -a
```

```bash
Linux black-pc 5.3.0-46-generic #38~18.04.1-Ubuntu SMP Tue Mar 31 04:17:56 UTC 2020 x86_64 x86_64 x86_64 GNU/Linux
```

```bash
brctl --version
```

```bash
bridge-utils, 1.5
```

### Création

- `sudo brctl addbr br0` : création d'un bridge nommé `br0`
- `brtcl show` : affiche la liste des bridges

#### Pré-process pour le wifi

```bash
# brctl addif <bridgename> <wifiInterface>
can't add <wifiInterface> to bridge <bridgename>: Operation not supported

# iw dev <wifiInterface> set 4addr on
# brctl addif <bridgename> <wifiInterface>
```

- `iw dev wlp3s7 set 4addr on` [ref](https://serverfault.com/questions/152363/bridging-wlan0-to-eth0)

#### ...suite pour ethernet et le wifi

- `sudo brctl addif br0 wlp3s7`

### Configuration permanente

```bash
cat /etc/network/interfaces
```

```bash
# interfaces(5) file used by ifup(8) and ifdown(8)
auto lo
iface lo inet loopback

# This file describes the network interfaces available on your system
# and how to activate them. For more information, see interfaces(5).

# Configurez les interfaces manuellement en évitant les conflits avec le manager réseau.
#iface enp2s0 inet manual

#iface enp3s6 inet manual

# Configuration du pont(bridge)
iface br0 inet dhcp
       bridge_ports wlp3s7
```

On peut désormais activer notre bridge `br0` via `ifup`

```bash
sudo ifup br0
```

qui renvoie

```
Waiting for br0 to get ready (MAXWAIT is 32 seconds).
Internet Systems Consortium DHCP Client 4.3.5
Copyright 2004-2016 Internet Systems Consortium.
All rights reserved.
For info, please visit https://www.isc.org/software/dhcp/

Listening on LPF/br0/90:f6:52:5b:3e:8a
Sending on   LPF/br0/90:f6:52:5b:3e:8a
Sending on   Socket/fallback
DHCPDISCOVER on br0 to 255.255.255.255 port 67 interval 3 (xid=0x8b6c0677)
DHCPREQUEST of 192.168.0.14 on br0 to 255.255.255.255 port 67 (xid=0x77066c8b)
DHCPOFFER of 192.168.0.14 from 192.168.0.254
DHCPACK of 192.168.0.14 from 192.168.0.254
cmp: EOF on /tmp/tmp.1dAYwgpvFE which is empty
bound to 192.168.0.14 -- renewal in 339536 seconds.
```

```bash
> brctl show
bridge name	bridge id		STP enabled	interfaces
br-85686f458148		8000.0242e0488d81	no
br0		8000.90f6525b3e8a	no		wlp3s7
docker0		8000.0242ba5f5869	no
virbr0		8000.5254005f3e88	yes		virbr0-nic
blackpc black-pc:/media/blackpc/Samsung USB/continuous-integration/doc
> ping www.google.fr
PING www.google.fr (172.217.19.227) 56(84) bytes of data.
64 bytes from par21s11-in-f3.1e100.net (172.217.19.227): icmp_seq=1 ttl=55 time=47.0 ms
^C
--- www.google.fr ping statistics ---
1 packets transmitted, 1 received, 0% packet loss, time 0ms
rtt min/avg/max/mdev = 47.033/47.033/47.033/0.000 ms
blackpc black-pc:/media/blackpc/Samsung USB/continuous-integration/doc
>
```

## Biblio

- [debian](https://wiki.debian.org/fr/BridgeNetworkConnections)
- [wikipedia STP](https://fr.wikipedia.org/wiki/Spanning_Tree_Protocol)
- [serverfault brctl iw](https://serverfault.com/questions/152363/bridging-wlan0-to-eth0)
- [rfwireless-world basics](https://www.rfwireless-world.com/Terminology/what-is-mac-address.html)
- [rfwireless-world bridge](https://www.rfwireless-world.com/Terminology/network-bridge.html)
- [help ubuntu bridge](https://help.ubuntu.com/community/NetworkConnectionBridge)
- [bridge exemple](https://linux.developpez.com/formation_debian/bridge.html)
