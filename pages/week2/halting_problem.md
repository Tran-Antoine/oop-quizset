---
layout: page
title:  "Halting problem avec des entiers"
---

Un **ou plusieurs** des codes ci-dessous terminent, et ce quelque soit la valeur de `x` passée en paramètre. Lesquels ?

A:
```java
void loop(int x) {
    for (int y = Math.abs(x); y != -1; ++y) x++;
}
```

B:
```java
void loop(int x) {
    int n = 0;
    for (int y = x; y != 0; y >>>= 1) n += y & 0x1;
}
```

C:
```java
void loop(int x) {
    while(x & -x == 0) {}
}
```

D.
```java
void loop(int x) {
    for(int i = x-1; i < x; i++) x++;
}
```

***

### Solution

- Dans le premier code, lorsque `y` atteint `Integer.MAX_VALUE`, l'incrémenter causera un overflow qui lui donnera la valeur `Integer.MIN_VALUE`. Il sera ensuite incrémenter jusqu'à atteindre `-1`, et la boucle s'arrêtera. Il convient de noter que l'instruction `x++` n'a aucune influence sur le résultat, car `int y = Math.abs(x)` n'est évalué qu'une seule fois, lors de l'entrée dans la boucle.

- Etant donné que le shift arithmétique vers la droite ajoute toujours des `0`, `y` finira forcément par devenir `0`, une fois que suffisamment de shifts sont effectués. La condition `y != 0` deviendra fausse et la boucle se terminera.

- Pour la valeur `x = 0`, la condition `x & -x == 0` est toujours vraie. La boucle ne se terminera donc pas.

- Dans ce dernier code, `i` et `x` vont être incrémentés jusqu'à ce que `x` atteigne `Integer.MAX_VALUE`, alors `i = Integer.MAX_VALUE - 1`. A la prochaine itération, `x` va overflow et passer dans les négatifs, il va donc prendre la valeur `Integer.MIN_VALUE` tandis que `i` prendra la valeur `Integer.MAX_VALUE`. Ainsi :
```java
i = Integer.MAX_VALUE > x = Integer.MIN_VALUE
```
Le programme se termine pour tout `x` passé en paramètre. 

Les réponses correctes sont donc les réponses **A**, **B** et **D**.


