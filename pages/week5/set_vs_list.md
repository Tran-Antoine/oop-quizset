---
layout: page
title:  "Notion d'ordre sur Set et List"
---


On définit la méthode suivante :

```java
<E> void printElems(Collection<E> elems) {
    for (E e : elems) {
        System.out.println(e.toString());
    }
}
```

Soient les codes suivants :

A.

```java
List<String> list = List.of("l'ovomaltine", "c'est", "de", "la", "dynamique");
printElems(list);
```

B.

```java
Set<String> set = new HashSet<>();
set.add("l'ovomaltine");
set.add("c'est");
set.add("de");
set.add("la");
set.add("dynamique");
printElems(set);
```

C.

```java
Set<String> set = new TreeSet<>();
set.add("l'ovomaltine");
set.add("c'est");
set.add("de");
set.add("la");
set.add("dynamique");
printElems(set);
```

Quelle affirmation est correcte ? Choisissez la réponse la plus précise.

A. A et B affichent la même chose

B. A et C affichent la même chose

C. B et C affichent la même chose

D. Tous les codes affichent la même chose

E. Tous les codes affichent quelque chose de différent


***

### Solution

Attention, c'est un piège très typique en programmation ! Une `List` est toujours ordonnée (donc le programme `A` affichera les mots dans l'ordre donné) mais un `Set` n'est pas (forcément) ordonné !

On peut d'ores et déjà éliminer les réponses A, B et D.

Ensuite, un `Set` peut aussi avoir un ordre différent en fonction de son implémentation. Tous les `Set` n'ordonnent pas leurs éléments de la même manière ! Nous n'avons donc aucune garantie sur l'ordre dans lequel les éléments seront affichés. En l'occurence, `B` et `C` affichent les éléments dans un ordre différent.

La réponse correcte est la `E`
