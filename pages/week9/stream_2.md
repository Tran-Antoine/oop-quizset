---
layout: page
title:  "Programmation par flots 2"
---

Déterminez le résultat du code suivant.

```java
boolean b = List.of(3,4,5,6)
    .stream()
    .anyMatch(x -> x > 5)
    .allMatch(x -> x > 2);
    
System.out.println(b);
```

A. true

B. Le code produit une erreur.

C. false

D. Le code ne compile pas.

***


### Solution

Ici `anyMatch` est une méthode terminale qui renvoie true si un des éléments de la liste est strictement plus grand que 5 et false dans le cas contraire. Etant donné qu'il est impossible d'appeller `allMatch` sur un booléen, le code ne va pas compiler, `allMatch` étant une méthode à appeler sur les streams.

La réponse est donc **D**.