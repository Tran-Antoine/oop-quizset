---
layout: page
title:  "Algèbre booléenne 2"
---

Vrai ou Faux ?

Après avoir exécuté le code suivant, l'expression `a → b` est une tautologie (est toujours vraie).

Partez du principe que `someMysteriousList` est une méthode valide qui renvoie une liste arbitraire de nombres, et que `someMysteriousPredicate` est une méthode valide qui renvoie un prédicat (`Predicate<Integer>`).

```java
List<Integer> list = someMysteriousList();
Predicate<Integer> predicate = someMysteriousPredicate();

boolean a = list
    .stream()
    .allMatch(predicate);

boolean b = list
    .stream()
    .anyMatch(predicate);
```

***

### Solution

Il est dans la plupart des cas vrai que si pour tout `x`, `P(x)` est satisfait, alors il existe un `x` tel que `P(x)` est satisfait. Malheureusement, cela n'est pas vrai dans le cas où `list` est une liste vide. Il est techniquement vrai que le prédicat est satisfait pour tout `x`, mais il n'existe aucun `x` tel que `P(x)` est satisfait, puisqu'il n'existe aucun `x` tout court. L'expression `a → b` est donc une contigence, mais non une tautologie. 

La réponse correcte est donc **Faux**