---
layout: page
title:  "Test d'immuabilité 4"
---

La classe suivante n'est pas immuable. Pourquoi ? Choisissez la proposition **la plus complète**.
```java
public class Zoo {

    private final List<Animal> animals;

    public Foo(List<Animal> animals) {
        this.animals = Collections.unmodifiableList(animals);
    }

    public List<Animal> getAnimals() {
        return new ArrayList<>(animals);
    }

    // autres méthodes privées utilisant l'attribut animals
}
```
A. Car la classe `Zoo` n'est pas déclarée `final`.
B. Car la classe possède un getter donnant accès à un attribut de la classe directement.
C. Car la classe `Animal` peut être muable
D. Car l'attribut `animals` peut être modifié
E. Pour les raisons A, C et D
F. Pour les raisons A, B et C
G. Pour les raisons A et C
H. Pour les raisons A et D
I. Pour toutes les raisons ci-dessus


***

### Solution

Afin de garantir l'immuabilité, il faut s'assurer que la classe soit `final`, autrement les sous-classes pourraient la briser.

Si la classe `Animal` se trouve être muable, il est tout à fait possible d'accéder, depuis l'intérieur **ou** l'extérieur, à un des objets de type `Animal` et de le modifier. Le fait qu'une copie de la liste soit effectuée avant d'être renvoyée dans le getter ne change rien à cela.

Malgré le fait que la classe `Zoo` n'ait accès qu'à une vue non-modifiable de la liste `animals`, la liste n'est en elle-même pas forcément immuable, elle peut être modifiée ailleurs dans le code. Cet exemple permet d'illustrer la situation:
```java
List<Integer> original = new ArrayList<>();
List<Integer> nonmodifiable = Collections.unmodifiableList(original);

System.out.println(nonmodifiable);
original.add(5);
System.out.println(nonmodifiable);
// Output: [] et [5]
```

Le fait que la classe possède un getter n'est pas un problème en soi, vu qu'une copie de la liste est effectuée à chaque fois.

La réponse correcte est donc la réponse **E**