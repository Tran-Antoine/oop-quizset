---
layout: page
title:  "Lecture de code 2"
---
Vrai ou Faux :

Si le test suivant passe, nous avons la garantie que la fonction `mySum`, qui calcule et renvoie la somme de tous les éléments d'un tableau de `double`s, est correctement implémentée.
> Note: `13.3 + 2.1 + 6.75 - 8.01 = 14.14`

```java
double[] array = {13.3, 2.1, 6.75, -8.01};
double sum = mySum(array);

assertEquals(14.14, sum, 1e-8);
```

### Solution

Etant donné que nous comparons des valeurs de type `double`, il est important de déterminer une certaine distance tolérée entre la valeur `expected` et `actual`, ce qui est correctement fait ici avec la valeur `1e-8` en troisième paramètre de `assertEquals`.

En revanche, le fait qu'une méthode passe un de nos tests ne nous donne aucune garantie
que cette méthode est implémentée correctement. Nous n'avons aucune idée de comment la méthode sum est implémentée. Il se peut très bien
que `mySum` ignore le tableau passé en paramètre et renvoie toujours `14.14`, ce qui passerait le test !

La bonne réponse est donc **Faux**