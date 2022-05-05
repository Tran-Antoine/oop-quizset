---
layout: page
title:  "Programmation par flots 7"
---

Determinez le type le plus précis de `mystery`.

```java
Object mystery = List.of("14", "76", "10")
    .stream()
    .mapToInt(Integer::parseInt)
    .max();
```

A: int / Integer
B: String
C: Autre
D: Le code ne compile pas.

***


### Solution

Ici on pourrait penser que `max` renvoie un objet de type int / Integer mais ce n'est pas le cas. On se retrouve bel et bien avec un stream de `Integer` avant l'appel à `max` mais cette fonction ne renvoie pas un `Integer` mais plutôt un `Optional<Integer>`. On est obligé de procéder ainsi car dans le cas ou le stream sur lequel on utilise `max` est vide, on ne peut pas déterminer quelle valeur retourner. `Optional<Integer>` est donc un objet qui "contient peut-être un Integer". Une manière simple d'unwrap un `Optional<T>` est d'utiliser la méthode `orElse(T other)` sur l'instance. Cette méthode va retourner l'objet contenu par l`Optional` si il contient bel et bien un élément et `other` sinon. Si on avait voulu que le code retourne bien un int / Integer, on aurait pu rajouter `.orElse(0)` après le `max` (et ici si le stream avait été vide, le résultat aurait été 0).

Il s'en suit donc, que la réponse est **C**.