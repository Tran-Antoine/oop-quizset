---
layout: page
title:  "Programmation par flots 4"
---

Déterminez le résultat du code suivant.

```java
boolean b = List.of("4", "7", "2")
    .stream()
    .map(Integer::parseInt)
    .anyMatch(x -> x > 6);
    
System.out.println(b);
```

A. Le code produit une erreur.

B. Le code ne compile pas.

C. true

D. false

***


### Solution

On convertit d'abord tous les String en l'Integer auquel ils corréspondent.
Ensuite on cherche simplement un élement qui remplit le prédicat "Est strictement plus grand que 6". Etant donné que le stream contient 7 qui est bien strictement plus grand que 6, `anyMatch` va retourner true.

La bonne réponse est donc **C**.