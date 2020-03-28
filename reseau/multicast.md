# Le multicast
_Quelques elements de base concernant la notion de multicast._

## Définitions
- connexion multipoint
  - unicast est en point à point (hote <---> hôte)
- application multicast 
  - hote <---> hote**S**
- groupe multicast : hote**S**
  - tous les participants de ce groupe
  - adresse de classe D : `224.0.0.0` -> `239.255.255.255`

## Plages d'adresses
|Adresses|Descriptions|
|----|----|
|`224.0.0.*`|utilisation locale sur le LAN|
|`224.0.0.1`|tous les hosts Xcasts du LAN|
|`224.0.0.2`|tous les routeurs Xcasts du LAN|
|`239.*.*.*`|administratively scoped addresses : adresses à portée locale|
> toutes les autres adresses ont une portée non limitée

## Notions importantes
- une adresse **multicast** ne peut-être que **destinataire**
- les **sources** ont toujours une adresse **unicast**

_Une source peut très bien envoyer à un groupe multicast sans en faire partie !!_
> Indépendance entre le fait d'être **membre** et de pouvoir envoyer

## Protocole IGMP
_Internet Group Management Protocol (`RFC 1112`)_

### Concernés
- les routeurs multicast du LAN
- les hôtes multicast du LAN

### Possibilités
- permet à un hôte de *s'abonner* / *desabonner* d'un groupe
  - le routeur fera suivre ou non les paquets multicast

### Principe
1. le routeur multicast envoie sur `224.0.0.1` un `IGMP Query` (périodique) (soit à tous les hôtes du LAN)
2. un hôte interessé repond par un `IGMP Report` au routeur

_Si plusieurs routeurs **multicast** alors un routeur dit `DR` (Designated Router) est le seul à pouvoir envoyer des `IGMP Query`_

## Biblio
- [PAU](http://cpham.perso.univ-pau.fr/ENSEIGNEMENT/COMMUN/multicast.pdf)
