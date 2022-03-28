Soit les 2 codes suivants :
A :
```java
List<Integer> l = new ArrayList<>();
for (int i = 0; i < Integer.MAX_VALUE; i++) {
    l.add(0, i);
}
```
B :
```java
List<Integer> l = new LinkedList<>();
for (int i = 0; i < Integer.MAX_VALUE; i++) {
    l.add(0, i);
}
```
Quel code est le plus rapide, d'un point de vue asymptotique ?
A. Le code A
B. Le code B
C. Ils se termineront presque en même temps

***

### Solution

Pour répondre à cette question, il faut se souvenir de l'implémentation d'une `ArrayList` et d'une `LinkedList`.

Une `ArrayList` contient un tableau d'éléments. Lorsqu'on ajoute un élément au début du tableau, nous sommes obligés de déplacer la totalité du tableau existant d'une place (pour faire de la place pour le nouvel élément). Cette opération se fait en `O(n)`.

Une `LinkedList` contient une suite d'éléments où chaque élément n'a connaissance que de son successeur (et parfois prédécesseur). Ainsi
si on note le nème élément par `n`, notre `LinkedList` ressemblerait à ça :
```
`0` -> `1` -> `2` -> ... `n`
```
Pour ajouter un élément `x` dans cette liste il suffit de faire en sorte que `x` "pointe" vers `0` et que la `head` de cette `LinkedList` soit mise à `x` :
```
`x` -> `0` -> `1` -> `2` -> ... `n`
```
Toutes ces opérations se font en `O(1)`

Ainsi, le programme `B` a asymptotiquement un temps d'exécution plus court que `A`.

La réponse correcte est la `B`
