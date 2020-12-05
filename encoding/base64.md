# Encodage en base64

Permet d'encoder l'information sur 64 caractères.

# Principe

Les caractères sont définis dans cet ordre

- 'A' - 'Z'
- 'a' - 'z'
- '0' - '9'
- '+'
- '/'

et un caractère reservé '=' pour effectuer des bourrages.

Chaque caractère est codé sur 6 bits (ce qui permet 2^6 possibilités, i.e. 64)

|index|définition sur 6 bits|caractère|
|-----|---------------------|---------|
|0    |000000               |A        |
|1    |000001               |B        |
|2    |000010               |C        |
|...  |...                  |...      |
|16   |010000               |Q        |
|...  |...                  |...      |
|25   |011001               |Z        |
|26   |011010               |a        |
|..   |...                  |...      |
|51   |110011               |z        |
|52   |110100               |0        |
|...  |...                  |...      |
|61   |111101               |9        |
|62   |111110               |+        |
|63   |111111               |/        |


### Prenons un exemple
- le caractère `A` correspond d'après la table ASCII à l'entier `65`
- `65` est représenté sur un octet comme suit : `01000001`
- l'encodage en base64 s'effectue sur 64 octets
    - le seul caractère `A` ne porte pas suffisamment d'informations.
    - d'où l'utilisation du caractère spéciale prévu `=` pour bourrer

|caractère|code ASCII|binaire   |base64                           |Commentaires                 |
|---------|----------|----------|---------------------------------|-----------------------------|
|`A`      |65        |`01000001`|010000 01 XXXX XXXXXX XXXXXX     |X correspond au bourrage     |
|         |          |          |010000 01`0000` `000000` `000000`|On bourre avec des zéro      |
- puis il suffit de décoder chacun des morceaux de 6bits dans l'ordre
    - 010000 > `Q`
    - 01`0000` > `Q`
    - `000000` > `=`
    - `000000` > `=`
    > Ce qui donne `QQ==`

# Pratique

## Commande : `openssl base64`

On peut simplement convertir une chaine de caractères avec la commande suivante

`echo -n "A" | openssl base64`

```bash
> echo -n "A" | python3 -m base64
QQ==
```

>Ne pas oublier de mettre l'option `-n` car sinon, un retour chariot avec retour à la ligne est réalisé...

```bash
user user-pc:/tmp/todelete 
> echo "A" | openssl base64
QQo=
user user-pc:/tmp/todelete 
> echo -n "A" | openssl base64
QQ==
user user-pc:/tmp/todelete 
> 
```

>Avec `QQ==` comme valeur attendue

## Python : `import base64`

Conversion directement en envoyant sur l'entrée std de la commande lançant python3 avec le module base64

`echo -n "A" | python3 -m base64`

```bash
> echo -n "A" | python3 -m base64
QQ==
```

## Python

Par l'intermédiaire d'un petit programme

On illustre ici l'encodage en binaire d'un message
Ce message pourra être vérifié en recherchant chaque morceau de 6 bits dans la table base64

```python
#!/usr/bin/env python3

import functools
import base64
import textwrap

msg = "coucou"
print(msg)

msg_to_list = list(msg)
print(msg_to_list)

msg_to_ascii = list(map(lambda letter: ord(letter), msg_to_list))
print(msg_to_ascii)

msg_to_bin = list(map(lambda ascii: "{0:b}".format(ascii), msg_to_ascii))
print(msg_to_bin)

msg_to_bin_8 = list(map(lambda to_8: "0" + to_8, msg_to_bin))
print(msg_to_bin_8)

msg_to_str = functools.reduce(lambda x, y: x + y, msg_to_bin_8)
print(msg_to_str)

msg_to_6 = textwrap.wrap(msg_to_str, 6)
print(msg_to_6)

# En regardant la table de correspondance de base64
# 011000 correspond à Y
# ... et finalement on obtient Y291Y291 pour le reste à traiter
# chunk_1 = int("011000", 2)
# print(chunk_1)

# On vérifie
dec_msg = base64.b64decode("Y291Y291")
print(dec_msg.decode())
```

L'exécution donne le résultat suivant

```bash
coucou
['c', 'o', 'u', 'c', 'o', 'u']
[99, 111, 117, 99, 111, 117]
['1100011', '1101111', '1110101', '1100011', '1101111', '1110101']
['01100011', '01101111', '01110101', '01100011', '01101111', '01110101']
011000110110111101110101011000110110111101110101
['011000', '110110', '111101', '110101', '011000', '110110', '111101', '110101']
coucou
```

# Biblio
- [wikipedia](https://fr.wikipedia.org/wiki/Base64)
- [python tutorial](https://pythonbasics.org/)
- [bvi sourceforge](http://bvi.sourceforge.net/quick.html)