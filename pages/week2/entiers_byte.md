---
layout: page
title:  "Entiers sur 8 bits"
---

Le code suivant compile-t-il ? Si oui, pourquoi ?
```java
byte question = 0b10001110;
```

A. Non, car un nombre donné avec le préfixe `0b` ne peut qu'être un `int`.

B. Non, car le nombre spécifié n'est pas entre la plus grande et la plus petite valeur représentable par le type `byte`.

C. Non, car la taille maximale d'un byte est de 4 bits, on ne peut donc pas lui assigner un nombre qui a une taille de 8 bits.

D. Oui, mais la compilation donne un **avertissement**.

E. Oui.

***

### Solution

En java, le type `byte` est un type servant à représenter des nombres entiers de 8 bits. On peut donc déduire que l'on peut représenter au plus `256` valeurs avec. Java encode les nombres entiers avec la technique du `2s complement`, ce qui veut dire que le bit de poids le plus fort correspond à une valeur négative. Ainsi, la plus petite valeur représentable d'un byte est `10000000`, qui est `-128`, alors que la plus grande valeur représentable est `01111111`, qui est `127`.

On pourrait donc penser que `10001110` correspond à `-128 + 8 + 4 + 2 = -114` et qu'il s'agit d'une valeur tout à fait valide pour un `byte`. Malheureusement, la notation Java `0b` suivie d'une séquence de bits est interprétée comme un **int** et non comme un `byte`. Les `int` étant des valeurs sur 32 bits, seul le 32ième bit (et non le 8ème !) est négatif. `10001110` correspond donc à `128 + 8 + 4 + 2 = 142`, qui est en dehors des valeurs que `byte` supporte.

La réponse correcte est donc la réponse **B**.