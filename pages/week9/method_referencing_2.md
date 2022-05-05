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


Alors que la deuxième syntaxe utilise du method referencing, `toUpperCase` est une fonction qui s'applique sur un string et prend donc un seul argument (le String sur le quel on l'applique). Dans ce cas on peut donc se servir de method referencing 

La réponse est donc **Vrai**.
