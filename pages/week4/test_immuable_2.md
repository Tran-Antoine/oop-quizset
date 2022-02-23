---
layout: page
title:  "Test d'immuabilité 2"
---

Vrai ou Faux:

Soit la classe `Warrior` suivante:
```java
public final class Warrior {
    private final int health;
    private final Sword sword;

    public Warrior(Sword sword, int health) {
        this.sword = sword;
        this.health = health;
    }

    public int health() {
        return health;
    }

    public Warrior withHealth(int newHealth) {
        return new Warrior(sword, newHealth);
    }
}
```
Alors, sachant qu'aucune supposition ne peut être faite à propos de la classe `Sword`, la classe `Warrior` est immuable.

***

### Solution

Malgré le fait que tous les attributs soient déclarés `final` et qu'aucune méthode de la classe ne cause de quelconque *mutation*, l'attribut de type `Sword` n'est pas copié dans le constructeur. S'il s'avère que `Sword` est une classe muable, l'attribut peut être modifié de l'extérieur.

La réponse correcte est donc **Faux**