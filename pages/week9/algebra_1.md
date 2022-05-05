---
layout: page
title:  "Algèbre booléenne 1"
---

Vrai ou Faux ? Le booléen `b` vaut `true`.

```java
List<String> list = new ArrayList<>();
boolean b = list
    .stream()
    .allMatch(x -> x == null);
System.out.println(b);
```

***

### Solution


L'opérateur `allMatch`, équivalent à `∀` en mathématiques, peut se traduire comme l'expression `¬(∃x ¬P(x))` (il n'existe pas de `x` tel que le prédicat échoue si testé avec `x` comme input). De cette manière, on voit que si la liste existe, il ne peut en effet pas exister de `x` qui fait échouer `P` et ce peu importe le prédicat, puisqu'il n'existe pas de `x` tout court. 

La réponse correcte est donc **Vrai**