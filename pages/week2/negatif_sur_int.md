---
layout: page
title:  "Int égaux à son négatif"
---

Soit `a` un `int`. Pour combien de valeurs de `a`, `-a == a` est évaluée à `true` ?

A. 0

B. 1

C. 2

D. 3 ou plus

***

### Solution

Il faut se rappeler que les `int` en java utilisent le complément à 2. Ainsi, le négatif
de `a` se calcule de cette manière :

```java
-a = ~a + 1
```

Ainsi, seules 2 `int` vérifient cette condition :
- `0` :
```java
0      = 0b00000000000000000000000000000000
~0     = 0b11111111111111111111111111111111 // -1 en décimal
~0 + 1 = 0b00000000000000000000000000000000 // en ajoutant 1, tous les bits seront mis à 0 à cause de la retenue, et le "33ème bit" sera mis à 1 (mais puisque celui-ci n'est pas représentable, on obtient bien 0)
```
- `Integer.MIN_VALUE` (-2147483648 qui est la plus petite valeur représentable) :
```java
-2147483648        = 0b10000000000000000000000000000000
~(-2147483648)     = 0b01111111111111111111111111111111 // 2147483647 qui est la plus grande valeur représentable en int
~(-2147483648) + 1 = 0b10000000000000000000000000000000 // en ajoutant 1, tous les bits seront à mis à 0 à cause de la retenue, et le 32ème bit sera mis à 1 (on retrouve le nombre de départ) ! C'est un overflow.
```

La réponse correcte est donc la réponse **C**
