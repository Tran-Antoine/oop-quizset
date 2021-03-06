---
layout: page
title:  "Intuition sur les lambdas"
---

> ⚠️ Cette question est un **bonus**. Elle teste votre intuition sur un sujet que vous n'avez pas encore abordé. Si vous ne savez pas y répondre, gardez-la pour la fin du semestre !

Comme expliqué dans le cours, il est possible de vérifier qu'une procédure résulte en une erreur, à l'aide de la syntaxe suivante:

```java
assertThrows(NoSuchElementException.class, () -> {
	doSomething();
      });
```

Mais en partant du principe que la méthode `doSomething` n'a pas comme type de retour `void`, pourquoi ne pas simplement faire:
```java
assertThrows(NoSuchElementException.class, doSomething());
``` 
?



A. Car `doSomething` peut renvoyer n'importe quel type d'objet, et il est impossible d'écrire une méthode `assertThrows` qui prend un objet de "n'importe quel type" en paramètre.

B. Car la première syntaxe permet d'effectuer plusieurs instructions à l'intérieur des `{}` (en les séparant par des `;`), mais pas la deuxième.

C. Dans ce cas précis cela aurait été possible, mais il existe des cas où l'on pourrait ajouter des paramètres à l'intérieur des `()` dans la syntaxe `() -> {...}` que la méthode `doSomething` aurait pu utiliser (par exemple `(int a) -> doSomething(a)`), chose qui n'est pas possible avec l'alternative proposée.

D. Car si `doSomething` lance une erreur, le programme crashera à l'exécution de l'instruction
```java
assertThrows(NoSuchElementException.class, doSomething());
```
et ce quelque soit l'implémentation de `assertThrows`. Cette étrange syntaxe permet donc d'encapsuler du code sans l'exécuter directement, un peu comme une fonction classique.

***

### Solution

Lors de l'évaluation d'une instruction et plus particulièrement l'évaluation d'une fonction, Java fonctionne avec un système appelé `call by value`. Simplement, cela veut dire que chaque argument de la fonction est évalué avant d'être passé en paramètre. Ceci implique que `doSomething()` sera réduit en une valeur de type `X` (en admettant que `X` est le type de retour de la fonction), puis passé à la fonction `assertThrows`. En y réfléchissant, cela n'a pas beaucoup de sens, pour plusieurs raisons:
- Si la fonction `doSomething` lance une erreur, le programme crashera avant même que `assertThrows` ne soit appelée
- Tout ce que la fonction `assertThrows` reçoit, c'est un objet d'un certain type. Comment pourrait-elle possiblement déterminer qu'une erreur a été lancée ou non ?
- Comment ferait-on si la méthode `doSomething` avait comme type de retour `void` ?

En réalité, la première syntaxe (appelée **lambda**) permet de définir une série d'instructions qui peut être stockée et utilisée plus tard, exactement comme une fonction. La méthode `assertThrows` peut donc s'occuper elle-même d'appeler le code en question quand elle le souhaite, probablement à l'intérieur d'un `try catch`. Si le bloc `catch` est utilisé, elle sait que le code "stocké" a lancé une erreur.

La réponse correcte est donc la réponse **D**