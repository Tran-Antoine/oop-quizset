---
layout: page
title:  "Programmation par flots 5"
---

Déterminez la sortie du code suivant.

```java
List<Integer> list = List.of("9", "16", "4")
    .stream()
    .map(Integer::parseInt)
    .sorted((a, b) -> Integer.compare(b, a))
    .collect(Collectors.toList());
    
System.out.println(list);
```

A. [16, 9, 4]

B. [4, 9, 16]

C. Le code produit une erreur

D [9, 16, 4]

***

### Solution

La première opération crée le stream. Ensuite, en utilisant de la référence de méthodes, on va transformer tous les `String` en la valeur `Integer` à la quelle ils corréspondent. Ensuite vient l'appel à sorted qui prend en argument un `Comparator`, ici nous utilisons simplement le comparateur offert par `Integer` mais avec un petit piège! Les deux arguments donnés à `compare` sont inversés, ce qui, comme vu en cours, correspond à un comparateur qui inverse l'ordre des int. Les éléments sont donc triés de manière décroissante! Finalement on fait appel à `collect` pour transformer le stream en liste triée de `Integer`.

Etant donné qu'on utilise un comparateur inversé, on obtient que la réponse est la **A**.