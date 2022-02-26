---
layout: page
title:  "Changement d'une région de bits"
---

Quel code ci-dessous permet de définir la valeur `b` aux bits d'index `i-1`, `i`, et `i+1` de `number` (considérant que `i = 0` est le bit le moins significatif) ? Pour raison de simplicité, vous pouvez partir du principe que `i` ne pointe pas vers un bit se trouvant à une des extrémités de `number`, et que bien que `b` soit de type `int`, il ne peut prendre que la valeur `0` ou `1`.

Par exemple, si `number = 00000000`, `i = 2`, `b = 1`, Alors `number` devrait devenir `00001110`.

> Note : Pour des raisons de clarté, certaines réponses sont divisés en plusieurs étapes.

A.
```java
int step1 = number & ~((1 << (i-1)) | (1 << i) | (1 << (i+1)))
int step2 = step1 | (b << (i-1)) | (b << i) | (b << (i+1));
number = step2;
```

B.
```java
int step1 = number & ~((1 << (i-1)) & (1 << i) & (1 << (i+1)));
int step2 = step1 & (b << (i-1)) & (b << i) & (b << (i+1));
number = step2;
```

C.
```java
int step1 = number | (b << (i-1)) | (b << i) | (b << (i+1));
number = step1;
```

D.
```java
int step1 = number & (0 << (i-1)) & (0 << i) & (0 << (i+1));
int step2 = step1 & (b << (i-1)) & (b << i) & (b << (i+1));
number = step2;
```

E.
```java
int step1 = number ^ (b << (i-1)) | (b << i) | (b << (i+1));
int step2 = step1 | (b << (i-1)) | (b << i) | (b << (i+1));
number = step2;
```

***

### Solution

Afin de changer la valeur d'un bit à un index `i` donné sans connaître `b` à l'avance, deux étapes sont nécessaires:
- Mettre le bit à l'index `i` à 0
- Effectuer l'opération `or` entre le bit à l'index `i` et `b`

Dans cet exercice, il y a 3 bits à changer. Afin de mettre les 3 à 0, il nous faut construire une masque contenant des `1` partout sauf aux 3 indexes correspondants, et appliquer l'opérateur `AND` entre la valeur et notre masque. Un tel masque peut être construit de la manière suivante:

- Constuire 3 masques contenant chacun un `1` à un des trois indexes (à l'aide de `<<`)
- Concaténer ces 3 masques (avec l'opérateur `&`)
- Inverser tous les bits du résultat (avec l'opérateur `~`)

Le masque est donc:
```java
~((1 << (i-1)) & (1 << i) & (1 << (i+1)))
```

Similairement, un masque contenant `b` aux 3 indexes en question, et `0` ailleurs peut-être construit de la manière suivante:
```java
(b << (i-1)) | (b << i) | (b << (i+1))
```
Il ne reste qu'à appliquer `AND` entre le nombre et le premier masque, puis `OR` entre le résultat et le second masque.

La réponse correcte est donc la réponse **A**