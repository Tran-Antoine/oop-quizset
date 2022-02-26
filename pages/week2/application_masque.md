---
layout: page
title:  "Application de masque"
---

Qu'affiche le code ci-dessous ?

> Note: `print8LSB` est une fonction donnée qui affiche les 8 bits les moins significatifs de l'entier passé en paramètre. Par exemple, `print8LSB(3)` devrait afficher `00000011`.

```java
int v = 0b10001101;
print8LSB(f(v));

int f(int v) {
	int mask = 0x7F & ~1;
	return v ^ mask;
}
```
A. 10001100


B. 01110010


C. 11110011


D. 10000001


E. 11111110

***

### Solution

Le masque est conçu par l'opérateur `AND` entre `0111 1111` (`7F`) et `1111 1110` (`~1`), et est donc `0111 1110`.

`1000 1101 XOR 0111 1110` = `1111 0011`. La réponse correcte est donc la réponse `C`.
