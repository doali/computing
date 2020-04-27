# SSH port forwarding

## Shéma de principe

![port-fowarding (linux france)](img/ssh-redirect.png)

## Cas pratique

![x -> y](img/ssh-xy.png)

### Scénario (cas tunnel renversé `-R` ou entrant)

Etant données les données présentes sur le schéma `x -> y`

- y tape la commande `ssh -p 22000 -R 22085:localhost:22001 u0_z82@192.168.0.11`

> créé une connexion SSH entre y et x sur le port `22000` initiée par y \
> créé un tunnel tel que

> - étant loggé sur `u0_z82@192.168.0.11`
> - toute connexion SSH adressée à localhost (loopback `127.0.0.1` de l'hôte `192.168.0.11)` sur le port `22085` sera redirigée sur le port `22001` de localhost qui a créé le tunnel (.i.e `192.168.0.12`)
> - sur l'hôte 192.168.0.11, par défaut, seule l'interface `loopback` est en écoute (ce qui explique la suite... `ssh -p 22085 localhost`)

- x tape la commande `ssh -p 22085 localhost`

> ce qui a pour effet de traverser le tunnel pour rejoindre `192.168.0.12` sur le port `22001`


## Biblio

- [linux-france schéma](http://www.linux-france.org/prj/edu/archinet/systeme/images/ssh-redirect.png)
- [fedora hôte visé résolution](https://doc.fedora-fr.org/wiki/Tunnels_SSH)
