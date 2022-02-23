---
layout: page
title:  "Lecture de code 1"
---
Vrai ou Faux:

Nous avons codé la méthode `myMin` suivante pour trouver le minimum d'un tableau:
```java
int myMin(int[] x) {
    return x[3];
}
```
Puisque nous sommes des programmeurs prudents, nous avons aussi écrit un test pour vérifier que notre méthode `myMin` fonctionne correctement:
```java
@Test
void method_min_works() {
    int[] x = new int[]{5, 6, 2, 0, 3, 7};
    assertEquals(correctMin(x), myMin(x));
}
```
Supposons que la méthode `correctMin` renvoie le minimum du tableau passé en paramètre. Ce test compile et s'exécute sans erreur.

***

### Solution

On peut d'un rapide coup d'œil déterminer que le min du tableau `x` est égal à 0.
Étant donné que la méthode `correctMin` est supposée correcte, on peut conclure qu'elle va retourner 0.
La méthode `myMin` quant à elle va pour déterminer le minimum aller chercher le quatrième élément du tableau.
Cet élément sera, avec le `x` donné, égal à 0. La méthode `assertEquals()` va donc comparer les deux éléments 
et conclure qu'ils sont égaux.

Vu que les deux éléments sont (par chance !) égaux le test va s'exécuter sans erreurs.
La bonne réponse est donc **Vrai**

Cette question illustre bien le fait que, même si notre méthode passe un test, on ne peut pas en conclure que 
le code fonctionne parfaitement. Il faut donc toujours se méfier des résultats de nos tests.