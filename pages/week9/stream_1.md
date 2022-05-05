---
layout: page
title:  "Programmation par flots 1"
---

Déterminez le résultat du code suivant.

```java
Collection<Integer> numbers = List.of(1,2,3,4);

List<Integer> result = numbers
    .stream()
    .filter(x -> x%2 == 0)
    .toList()

System.out.println(result); 
```

A. [1, 2, 3, 4]

B. [1, 3]

C. [2, 4]

D. Le code compile mais lance une erreur à l'exécution

E. Le code ne compile pas

***

### Solution


On crée en premier lieu une collection contenant les nombres de 1 à 4. Puis on applique un filtre, en ne laissant que passer les nombres pairs (c'est à dire les nombres dont le résultat de la division entière par 2 vaut 0). Une fois le filtre effectué, on convertit le stream en une liste, qu'on affiche.

La réponse correcte est donc la réponse **C**.