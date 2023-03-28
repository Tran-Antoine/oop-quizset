---
layout: page
title:  "Itération sur des listes"
---

On considère un objet `l` de type `List<Integer>`. On suppose que la taille de l est très grande.

A.
```java
for (int i = 0; i < l.size(); i++) {
    System.out.println(l.get(i));
}
```
B.
```java
for (int elem : l) {
    System.out.println(elem)
}
```
Quelle affirmation est correcte ? Choisissez la réponse la plus précise.

A. Si `l` a pour implémentation `ArrayList<Integer>`, alors les 2 codes auront asymptotiquement le même temps d'exécution

B. Si `l` a pour implémentation `LinkedList<Integer>`, alors les 2 codes auront asymptotiquement le même temps d'exécution

C. Peu importe l'implémentation de `l`, les 2 codes auront toujours asymptotiquement le même temps d'exécution

D. Peu importe l'implémentation de `l`, les 2 codes n'auront jamais asymptotiquement le même temps d'exécution

***

### Solution

Pour répondre à cette question, il faut se souvenir des implémentations de `ArrayList` et `LinkedList`.

Une `ArrayList` ne fait que contenir un tableau d'éléments. Ainsi tous les appels à `l.get(i)` sont "équivalents" en temps d'exécution à simplement retrouver le ième élément d'un tableau (`array[i]`), cette opération se fait en `O(1)` (temps constant). Donc le programme `A` s'exécute en `O(n)` avec une `ArrayList`.

Une `LinkedList` contient une suite d'éléments où chaque élément n'a connaissance que de son successeur (et parfois prédécesseur). Ainsi
si on note le nème élément par `n`, notre `LinkedList` ressemblerait à ça :
```
`0` -> `1` -> `2` -> ... `n`
```
Pour accéder à l'élement `i`, nous sommes obligés de passer d'abord par `0`, `0` nous mènera à `1`, `1` nous mènera à `2` etc. jusqu'à `i` (un peu comme une chasse au trésor :)). Donc `l.get(i)` s'exécute en `O(i)` où `i` est l'index de l'élement. Ainsi, le programme `B` s'exécute en `O(n²)` (après des calculs d'AICC 1 :P).

**MAIS** le programme `B` ne fait pas d'appel à `get`. Le programme `B` utilise la notion d'itérateur. Pour faire court, un itérateur n'est qu'un marque-page, il est facile de connaitre l'élement courant et le prochain élément. Avec cette implémentation, on peut retrouver le prochain élément en `O(1)` peu importe l'implémentation de la liste. Ainsi le programme `B` s'effectuera toujours en `O(n)`.

C'est pour cela que la syntaxe du programme `B` est toujours préférable à la `A` dans la mesure du possible.

La réponse correcte est la `A`