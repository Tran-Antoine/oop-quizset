---
layout: page
title:  "Immuable vs non modifiable"
---

On définit les 2 classes suivantes :
```java
class A {...}
final class B extends A {...}
```

Et le code suivant :
```java
A a = new B();
someMysteriousFunction(a);
```

Sachant qu'il n'existe aucune implémentation possible de `someMysteriousFunction` qui **n'utilise pas de transtypage (aka "cast")** tel que le code ci-dessus modifie `a`, quelle proposition est vraie ?
Choisissez la proposition la plus complète.

A. La classe `A` est immuable

B. La classe `B` est immuable

C. La classe `A` est non-modifiable

D. La classe `B` est non-modifiable

E. Les propositions A et C

F. Les propositions B et D

***

### Solution

On sait déjà que immuable implique non-modifiable, ce qui nous permet d'éliminer les réponses A et B.


__Est-ce que `A` est immuable ?__

Puisque `A` est n'est pas `final`, `A` n'est pas immuable.


__Est-ce que `B` est immuable ou non-modifiable ?__

Rien ne peut être dit sur `B`. Considérons le code suivant :
```java
class A {
    // corps vide
}

final class B extends A {
    private int x = 0;
    
    public void setX(int newX) {
        this.x = newX;
    }
}
```
Dans cet exemple, `B` n'est évidemment ni immuable ni non-modifiable puisque tout morceau de code ayant accés à un objet de **type déclaré** `B` peut modifier cet objet avec `setX`. Mais `someMysteriousFunction` n'a accés qu'aux méthodes de `A` et ne peut donc pas agir sur l'objet `a` passé en paramètre, donc `a` ne pourra pas être modifié.


(Par élimination, nous pouvons cocher la réponse **C** :))


__Pourquoi `A` est non-modifiable ?__

`someMysteriousFunction` peut représenter n'importe quelle fonction. Admettons qu'elle soit malicieuse et cherche à tout prix à modifier l'objet `a` passé en paramètre. On nous affirme que `someMysteriousFunction` n'est pas capable de modifier `a` donc, elle ne peut pas appeler de méthode modifiant `a`. `A` est donc non-modifiable. 

La réponse correcte est donc la réponse **C**
