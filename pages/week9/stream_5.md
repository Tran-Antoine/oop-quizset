---
layout: page
title:  "Programmation par flots 5"
---

Déterminez le résultat du code suivant.

```java
Collection<Integer> numbers = List.of(3, 2, 9, 0);

int result = numbers
    .stream()
    .map(x -> x + 1)
    .flatMap(x -> Arrays.asList(x, x + 1).stream())
    .distinct()
    .reduce((a, b) -> a+b)
    .orElse(-1);

System.out.println(result);
```

A. 18

B. 36

C. 32

D. Le code compile mais lance une erreur à l'exécution

E. Le code ne compile pas

***

### Solution


Listons les différentes opérations que nous appliquons:

- Ajout de un à chaque nombre

`[3, 2, 9, 0]` => `[4, 3, 10, 1]`

- Conversion de chaque valeur x en un tuple (x, x+1), aplati

`[4, 3, 10, 1]` => `[(4, 5), (3, 4), (10, 11), (1, 2)]` => `[4, 5, 3, 4, 10, 11, 1, 2]`

- Suppression des dupliqués 

`[4, 5, 3, 4, 10, 11, 1, 2] => [4, 5, 3, 10, 11, 1, 2]`

- Réduction en somme des éléments

`[4, 5, 3, 10, 11, 1, 2] => 4 + 5 + 3 + 10 + 11 + 1 + 2 = 36`

- Récupération du résultat si présent, sinon -1

`36 => 36`


La réponse correcte est donc la réponse **B**.