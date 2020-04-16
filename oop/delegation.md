# Délégation et héritage

```text
Déléguer une tâche revient à la confier à quelqu’un d’autre. Ainsi, en OOP, un objet peut confier la résolution d’une de ses opérations à un autre objet. L’objet endossant cette responsabilité est nommé le delegate (ou délégué). Le rôle d’un delegate est de définir du comportement laissé à charge.

    Java, dans ses bibliothèques standards, a recours à une version « classique » de la délégation. Comme l’énonce le pattern éponyme : une classe, au lieu d’implémenter une de ses opérations, mandate un helper — le delegate — pour ce faire ;
    Une version « inversée » de la délégation, plus méconnue, permet à une classe de créer une déclinaison d’une autre classe adaptée à la situation. Cette dernière déclare qu’une partie de son comportement est indéfini et doit être fourni lors de son utilisation. Lorsqu’une classe l’utilise — elle est delegate — elle accepte de définir ce comportement délégué.
    En d’autres termes : lorsqu’une classe A utilise une classe B, elle est à même de définir une partie du comportement de B. La partie en question est déterminée par B.

Contrairement à la version « classique » ou une classe confie une opération à une autre, dans la version « inversée » une classe laisse la charge d’une partie de son comportement à celles l’utilisant.
```

> repris de : Yves Amsellem

## Biblio

- [publicissapient delegation](https://blog.engineering.publicissapient.fr/2011/01/17/de-lheritage-a-la-delegation/)
