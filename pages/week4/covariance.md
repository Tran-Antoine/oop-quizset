---
layout: page
title:  "Introduction à la covariance"
---

Considérez l'ensemble de classes suivant:

- Une classe `Animal` quelconque
- Une classe `Canine` qui hérite de `Animal` (donc `Canine extends Animal`)
- Une classe `Dog` qui hérite de `Canine` (donc `Dog extends Canine`)
- Une classe `Cell` qui possède un paramètre générique `T` qui hérite de `Animal`  (`class Cell<T extends Animal> {...}`)

On définit une méthode `foo` avec la signature suivante:
```java
public void foo(Cell<Canine> cell) {...}
```

Quels objets sont des paramètres acceptables de la méthode `foo` ? Choisissez la réponse la plus précise.

A. Un paramètre de type `Cell<Animal>`

B. Un paramètre de type `Cell<Canine>`

C. Un paramètre de type `Cell<Dog>`

D. Les réponses A et B

E. Les réponses B et C

F. Toutes les réponses ci-dessus

***

### Solution

Un piège très typique qui peut paraître très illogique au premier abord !

Il semble plutôt normal que `Cell<Aniaml>` ne soit pas un paramètre valide. Il s'agit d'un type "valide", dans le sens où le paramètre générique d'une cellule doit hériter de `Animal`, et c'est bien le cas ici. En revanche, la méthode `foo` demande une cellule de type `Canine`, qui est un type plus précis que `Animal`. `Cell<Animal` n'est donc pas un paramètre acceptable. Similairement, si la méthode `foo` demandait un objet de type `Apple`, il ne serait pas possible de fournir un `Fruit`, qui est un type plus général. On peut donc éliminer les réponses `A`, `D` et `F`.

Il est trivial de noter que `Cell<Canine>` est bien évidemment un paramètre valide, puisqu'un `Cell<Canine>` est demandé.

Quand à `Cell<Dog>`, sachant que `Dog` hérite de `Canine`, est-ce un paramètre valide ? Pour le comprendre, il s'agit de déterminer quelles conditions doivent être remplies pour pouvoir être un paramètre acceptable. Soit une méthode demandant un objet de type `X`. Un objet de type `Y` est un paramètre valide, si une des deux conditions suivantes est remplie:

- `X` = `Y`
- `Y` hérite de `X`

Par exemple, s'il est demandé de fournir un `Animal`, il est tout à fait raisonnable de fournir un `Dog` (en partant du principe que `Dog extends Animal`, puisque par héritage, un chien se doit de remplir toutes les caractéristiques d'un animal (ce qui est important, car une méthode demandant un `Animal` se réserve le droit de faire tout ce que la classe `Animal` donne à disposition, et ceci doit rester vrai même si un `Dog` est passé en paramètre). En d'autres termes, même si le type le plus "précis" est `Dog`, il est tout à fait possible de **visualiser** un chien comme "un animal quelconque", ce qui le rend un paramètre valide.

Pour revenir à nos moutons, il est évident que `Cell<Dog>` et `Cell<Canine>` ne sont pas "identiques". La question est donc: est-ce que `Cell<Dog>` est un sous-type de `Cell<Canine>` ? En d'autres termes, peut-on **visualiser** un objet de type `Cell<Dog>` comme un objet de type `Cell<Canine>`, et faire tout ce qu'un `Cell<Canine>` peut faire avec ? Il se trouve que la réponse est non. Prenons l'exemple de classe `Cell` suivant:

```java
public class Cell<T extends Animal> {


    private T animal;

    public Cell(T animal) {
        this.animal = animal;
    }

    public void set(T newAnimal) {
        this.animal = newAnimal;
    }

    public T get() {
        return animal;
    }
}
```

Et imaginons la méthode `foo` suivante:

```java
public void foo(Cell<Canine> cell) {
    cell.set(new Wolf());
}
```

Que se passe-t-il si on lui donne un objet de type `Cell<Dog>` en paramètre ? Notre cellule contenant un chien se retrouverait avec un loup à l'intérieur... ce serait un bug majeur dans notre programme: une méthode qui doit renvoyer un chien renverrait subitement un loup, malgré que ces deux types n'aient rien à voir (ou du moins l'un n'est pas une sous classe de l'autre) !

Pour cette raison, le fait que `A` extends `B` n'implique **pas** que `SomeGeneric<A>` extends `SomeGeneric<B>` ! `Cell<Dog>` n'est donc pas un paramètre valide.

La réponse correcte est donc la réponse **B**.
