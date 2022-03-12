---
layout: page
title:  "Multiple généricité bornée"
---

Soit l'interface `FoodFunction` possédant une fonction `apply` décrite ci-dessous.
```java
public interface FoodFunction<???> {

    public ??? apply(???);

}
```

Les `???` représentent du code manquant, qui doit être complété. On souhaite que l'interface fonctionne de la manière suivante: elle prend en paramètre un ingrédient brut, qui doit hériter de `RawIngredient`, et renvoie un plat préparé, qui doit hériter de `CookedMeal`. Il s'agit donc d'une interface permettant de "convertir" un ingrédient en un plat, via la méthode `apply`. Notez que `FoodFunction<RawIngredient, CookedMeal` est un type valide, mais ce n'est pas le seul. `FoodFunction<Apple, ApplePie>` par exemple doit également en être un, et le code suivant doit compiler:
```java
FoodFunction<Apple, ApplePie> f = (...);
ApplePie result = f.apply(new Apple());
```
Comment faut-il compléter les `???` ? (dans l'ordre, donc d'abord le/les type générique de `FoodFunction`, puis le type de retour de `apply`, puis le type de paramètre de `apply`)

A. `RawIngredient, CookedMeal`, `CookedMeal`, `RawIngredient`

B. `P extends RawIngredient, R extends CookedMeal`, `CookedMeal`, `RawIngredient`

C. `P extends RawIngredient, R extends CookedMeal`, `P`, `R`

D. `P, R extends CookedMeal`, `<P extends RawIngredient> P`, `R`

E. `P extends CookedMeal, R`, `<R extends CookedMeal> P`, `R`

F. `P extends RawIngredient, R extends CookedMeal`, `<S extends RawIngredient, T extends CookedMeal> S`, `T`


***

### Solution

Procédons par élimination. La réponse `A` n'a aucun sens: si on met directement `RawIngredient` et `CookedMeal` entre les `<>`, ils correspondront simplement à des noms de types génériques, sans **aucun** rapport avec les **classes** `RawIngredient` et `CookedMeal`. Donc les deux codes suivants:
```java
public interface FoodFunction<RawIngredient, CookedMeal> {...}
```
et
```java
public interface FoodFunction<A, B> {...}
```
sont **complètement** (!!!) équivalents, la seule différente étant les noms des types génériques.

Les types génériques de la réponse `B` sont déjà bien plus corrects, malheureusement le type de retour de la fonction ainsi que le type de paramètre sont trop généraux: admettons que nous avons une `FoodFunction<Orange, OrangeJuice>`, il est possible de lui donner un `Steak` en paramètre, et on ne peut rien récupérer de plus précis qu'un `CookedMeal`, malgré le fait qu'on souhaiterait pouvoir récupérer un `OrangeJuice`.

La réponse `D` est fausse, puisqu'il est possible de créer une `FoodFunction<Tractor, Lasagna>`, étant donné qu'il n'y a aucune restriction sur `P`. Le fait que `apply` demande un type `P` borné par `P extends RawIngredient` ne fait qu'empirer les choses: l'utilisateur de la méthode peut fournir n'importe quelle sous-classe de `RawIngredient`, mais la fonction elle-même n'a pas connaissance du type précis donné, il ne peut que se baser sur ce que `RawIngredient` propose. De plus, même s'ils ont le même non, le `P` défini au niveau de la classe et celui défini comme paramètre générique de la méthode n'ont rien à voir.


La réponse `E` est fausse pour une raison similaire à la `D`.

La réponse `F` est fausse, car le type de retour / paramètre de la fonction `apply` étant déconnectés des paramètres `P` et `R` définis au niveau de la classe, il est possible de lancer le code suivant:

```java
FoodFunction<Pasta, Carbonara> f = (...);
Caramel result = f.apply(new Sugar());
```

De plus, il est complètement impossible d'écrire l'implémentation de `apply`, vu qu'elle devrait pouvoir gérer n'importe quel combinaison de type paramètre + retour, autant `Apple` et `ApplePie` que `Chocolat` et `Cake`, que `Flour` et `Bread`, etc.

La réponse `C`, en revanche, est correcte: les deux types génériques sont libres mais bornés par `RawIngredient` et `CookedMeal`, le type de retour et de paramètres sont les mêmes que ceux spécifiés au niveau de la classe.

La réponse correcte est donc la réponse **C**.