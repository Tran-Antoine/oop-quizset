---
layout: page
title:  "Lecture de code 2"
---
Vrai ou Faux :

Si le test suivant passe, nous avons la garantie que la fonction `mySum`, qui calcule et renvoie la somme de tous les éléments d'un tableau de `double`s, est correctement implémentée.
> Note: `13.3 + 2.1 + 6.75 - 8.01 = 14.14`

```java
int[] array = {13.3, 2.1, 6.75, -8.01};
int sum = mySum(array);

assertEquals(14.14, sum, 1e-8);
```

### Solution

Le fait qu'une méthode passe un de nos tests ne nous donne aucune garantie
que cette méthode est implémentée correctement. En l'occurrence, il n'y a aucune erreur liée
aux opérations et comparaisons sur des `double`s puisque la note nous informe que la
somme donne le résultat escompté, et nous avons pris le soin d'ajouter un "delta" (3ème argument
de `assertEquals`) qui nous donne une marge d'erreur lors de la comparaison de `double`s.

En revanche, nous n'avons aucune idée de comment la méthode sum est implémentée. Il se peut très bien
que `mySum` ignore le tableau passé en paramètre et renvoie toujours `14.14`, ce qui passerait le test !

La bonne réponse est donc **Faux**