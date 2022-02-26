---
layout: page
title:  "Entiers égaux à leur négatif"
---

Soit `a` un entier de type `int`. Pour combien de valeurs de `a` est-ce que le booléen `-a == a` est-il `true` ?

A. 0

B. 1

C. 2

D. 3 ou plus

***

### Solution

Il faut se rappeler que les `int` en java utilisent le complément à 2. Ainsi, l'opposé de `a` se calcule de cette manière :

```java
-a = ~a + 1
```

Sachant cela, il n'est pas si intuitif, mais vrai, que la valeur `0` soit égale à son opposé:

```java
0      = 0b00000000000000000000000000000000
~0     = 0b11111111111111111111111111111111 // = -1 en décimal
~0 + 1 = 0b00000000000000000000000000000000 // en ajoutant 1, tous les bits seront mis à 0 à cause de la retenue, et le "33ème bit" sera mis à 1 (mais puisque celui-ci n'est pas représentable, il est ignoré (overflow)
```

Mais attention, une autre valeur vérifie également cette condition. En effet, dans le complément à 2, on peut représenter plus de nombres négatifs que de nombres positifs (il y'a un nombre négatif de plus !). Ainsi `-Integer.MIN_VALUE = 2147483648` n'est pas représentable en `int`. Voyons voir ce qu'il se passe :

```java
-2147483648        = 0b10000000000000000000000000000000
~(-2147483648)     = 0b01111111111111111111111111111111 // 2147483647 qui est la plus grande valeur représentable en int
~(-2147483648) + 1 = 0b10000000000000000000000000000000 // en ajoutant 1, tous les bits seront à mis à 0 à cause de la retenue, et le 32ème bit sera mis à 1. Mais le 32ème bit correspond à la valeur négative 2^-31 ! On retrouve donc le nombre de départ.
```

Ainsi, `Integer.MIN_VALUE` possède également la propriété `a = -a`.

La réponse correcte est donc la réponse **C**
