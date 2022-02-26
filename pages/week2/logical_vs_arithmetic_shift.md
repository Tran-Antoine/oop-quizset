---
layout: page
title:  "Décalage logique vs décalage arithmétique"
---

Qu'affiche le programme suivant ?
```java
System.out.println(-2 >>> 1);
```

A. 1

B. -1

C. 2147483647

D. -2147483647

***

### Solution 

Attention à ne pas tomber dans le piège, ici on utilise un décalage **logique** (et non arithmétique) qui ne fait qu'insérer des bits nuls à gauche. Voilà la représentation de `-2` en binaire :
```
-2 = 0b11111111111111111111111111111110
```
En décalant vers la droite de 1, et en insérant un bit nul à gauche :
```
-2 >>> 1 = 0b01111111111111111111111111111111
```
On obtient la plus grande valeur représentable par un `int` qui est 2147483647.

La réponse correcte est donc la réponse **C**
