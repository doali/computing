# Transmission

- sens des échanges (émetteur <-> récepteur)
- mode de transmission (série, parallèle)
- synchronisation (asynchrone, synchrone) 
- parité

## Sens des échanges

|circulation \ liaison|simplex  |half-duplex         |full-duplex        |
|---------------------|---------|--------------------|-------------------|
|sens                 |->       |<-> (par alternance)|<-> (simultanément)|


## Mode de transmission

|liaison|N bits|lien physique|
|-------|-----------|-----------|
|parallèle|simultanément|N voies différentes (fils, nappes, ...)|
|série|les uns à la suite des autres|1 voie|

_Dans le cas où l'on émet en parallèle et que l'on souhaite envoyer en série ou bien inversement, on utilise une puce UART_

- puce `UART` (Universal Asynchronous Receiver Transmitter)
    - serie -> parallèle : registre de décalage, on remplit N bits et on envoie
    - parallèle -> série : registre de décalage, on envoie dans l'ordre (implique horloge) les N bits reçus simultanéments

## Synchronisation

- asynchrone
    - émission irrégulière de caractères (8 bits)
    - bit START et bit STOP
      afin d'être en mesure de delimiter les 8 bits envoyés pour que le caractère soit reconnu

- synchrone
    - émetteur et récepteur sont cadencés à la même horloge

## Parité

Dans le cadre de la manipulation de liaisons séries, pour effectuer des contrôles sur les données, on réalise une **somme de contrôle**.

### Somme de contrôle

la **parité** vaut

- 1 : si le nombre de bits à 1 est *impair*
- 0 : sinon

- [doali parity.c](https://github.com/doali/coding/blob/master/c/coding/var/type/parity.c)


# Biblio

- [linux-france](http://www.linux-france.org/prj/edu/archinet/systeme/ch02s03.html)
- [geeksforgeeks vocabulary](https://www.geeksforgeeks.org/network-devices-hub-repeater-bridge-switch-router-gateways/)
- Linux Magasine HS 70
- [transmission CCM](https://web.maths.unsw.edu.au/~lafaye/CCM/transmission/transmode.htm)
- [marseille](http://www.pedagogie.ac-aix-marseille.fr/upload/docs/application/pdf/2015-02/transmission_serie.pdf)
