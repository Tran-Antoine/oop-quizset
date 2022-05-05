---
layout: page
title: "Référence de méthode 2"
---

Vrai ou Faux :  

Les deux codes suivants sont équivalents.

```java
Function<String, String> func = str -> str.toUpperCase();
```
```java
Function<String, String> func = String::toUpperCase;
```

***

### Solution


La première syntaxe définit une fonction qui prend un String `str` en paramètre et renvoie le résultat de `str.toUpperCase()`


La deuxième syntaxe utilise du référençage de méthode: `toUpperCase` est une fonction qui s'applique sur un String et ne prend aucun argument, si ce n'est le String sur lequel on l'applique. Il s'agit donc d'une écriture complètement équivalente à la première.


La réponse est donc **Vrai**.
