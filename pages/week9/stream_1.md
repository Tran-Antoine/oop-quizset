---
layout: page
title:  "Programmation par flots 1"
---

Déterminez le résultat du code suivant.

```java
Stream<Integer> stream = List.of(1, 2, 3, 4, 5).stream();


List<Integer> list1 = stream
    .filter(x -> x <= 4)
    .toList()

List<Integer> list2 = stream
    .filter(x -> x >= 2)
    .toList()

List<Integer> total = new ArrayList<>();
total.addAll(list1);
total.addAll(list2);

System.out.println(total);
```

A. [1, 2, 3, 4, 2, 3, 4, 5]

B. [5, 1, 2]

C. Le code compile mais lance une erreur à l'exécution

D. Le code ne compile pas



***

### Solution


Il existe plusieurs types d'opérations sur les streams. Certaines permettent d'en créer un (`Stream.of`, `list.toStream`, etc), certaines passent d'un stream à un autre (`map`, `flatMap`, `filter`, etc), et d'autres génèrent un résultat concret (`reduce`, `toList`, `max`, etc).

Il est important de noter que les opérations générant un résultat sont **terminales**. Elles doivent être la dernière action effectuée, et le stream est fermé après cette dernière, de manière définitive. Pourtant, dans le code ci-dessus, on réutilise `stream` après avoir appliqué `toList` une première fois, ce qui est interdit.

La réponse correcte est donc la réponse **C**.
