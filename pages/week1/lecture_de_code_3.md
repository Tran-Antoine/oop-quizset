---
layout: page
title:  "Lecture de code 3"
---
Vrai ou Faux :

> Note: Lorsque nécessaire, partez du principe que `someRandomArrayOfInts` renvoie un tableau de taille aléatoire non nulle contenant des entiers aléatoires.

Nous avons codé la méthode `myMean` qui renvoie la moyenne d'un array de int (sous forme de double). Puisque nous sommes des programmeurs prudents, nous avons aussi écrit un test unitaire pour vérifier que notre méthode `myMean` fonctionne correctement:
```java
@Test
void method_mean_works() {
    for (int i = 0; i < 1000; i++) {
        int[] x = someRandomArrayOfInts();
        assertEquals(((double) correctSum(x)) / x.length, myMean(x), 1e-8);
    }
}
```
Supposons que la méthode `correctSum` renvoie la somme de l'array de int passé en paramètre. 
Alors ce test unitaire est robuste face aux erreurs d'implémentation (i.e il a de grandes chances de détecter une erreur si `myMean` est mal implémentée)

### Solution

Cete question est un bon exemple de test robuste face aux erreurs d'implémentation :
- Il teste une grande variété de tableaux et a donc de grandes chances de tomber sur un cas qui ne fonctionne pas si `myMean` est mal implémentée
- Le résultat de `myMean` est comparé à un résultat vrai déjà connu. En l'occurrence, nous savons que `correctSum` renvoie
la somme correcte de le tableau passé en paramètre et nous avons utilisé la bonne définition de la moyenne
- Nous avons pris soin d'ajouter le 3ème argument "delta" à `assertEquals` puisque nous comparons des `double`s

Par souci de complétude, nous aurions dû vérifier les cas limites (i.e que se passe-t-il si le tableau est vide par exemple ?),
mais puisque le comportement attendu de `myMean` est ambigu, nous avons choisi d'ommettre cette possibilité pour cette question. Bien sûr, dans la pratique, il faut toujours tester les cas limites :)

Réponse : **Vrai**