---
layout: page
title:  "Référence de méthode 1"
---

On définit l'interface ci-dessous.
```java
interface MyInterface {

    String action();

}
```

Déterminez le résultat du code suivant.

```java
MyInterface test = String::toLowerCase;
System.out.println(test.action("ALL_CAPS"));
```


A. ALL_CAPS

B. all_caps

C. Le programme compile mais lance une erreur à l'exécution

D. Le programme ne compile pas

***

### Solution


`MyInterface` est une interface fonctionnelle représentant une fonction de type `() -> String`. Or, `String::toLowerCase` est équivalente à une fonction `String -> String`, et ce malgré le fait que `toLowerCase` ne prenne aucun paramètre ! En effet, étant donné qu'il s'agit d'une méthode d'instance, la chaîne de caractères en question depuis laquelle `toLowerCase` est appliquée est considérée comme un paramètre. Deux solutions sont possibles pour régler le problème:

- Ajouter un paramètre `String` à la méthode `action`
- Remplacer le code par:
```java
// puisqu'on spécifie le String en question, pas besoin de le passer en paramètre
MyInterface test = "ALL_CAPS"::toLowerCase; 
System.out.println(test.action());
```

La réponse correcte est donc la réponse **D**.
