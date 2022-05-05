---
layout: page
title:  "Référence de méthode 3"
---

title = "Lambda vs method referencing"
text = '''
Vrai ou Faux: 
Les deux codes suivants sont équivalents.
```java
Function<String, Integer> func = str -> str.length();
```
```java
Function<String, Integer> func = str::length;
```

***


### Solution

La méthode `length` de la classe String est une méthode qui ne prend aucun paramètre, mais est une méthode d'instance. Ici, avec la notation actuelle, `length` devrait s'appliquer sur le String `str` et simplement renvoier sa longueur. Il s'agit donc d'une fonction de type `() => Integer`. Malheureusement, `Function<String, Integer>` représente une fonction `String => Integer`, qui n'est donc pas le même type de fonction. Pour cette raison le code ne compile pas.

La réponse est donc **Faux**.
