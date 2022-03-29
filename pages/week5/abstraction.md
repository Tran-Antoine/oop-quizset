---
layout: page
title:  "Abstraction des collections"
---

Considérez les deux codes suivants:

```java
ArrayList<String> list = new ArrayList<>(1);
list.add("Hello");
```
```java
public void print(ArrayList<String> list) {
    for(String s : list) {
        System.out.println(s);
    }
}
```

De manière générale, serait-il préférable de remplacer le type **déclaré** (donc sans compter l'instanciation `new ArrayList<>()`) des variables `list` en `List` à la place de `ArrayList` ? (en admettant que cela soit possible, c'est à dire que le code compile toujours après)
 
A. Non, dans aucune circonstance le code compilera-t-il, puisque `List` et `ArrayList` ne sont pas le même type (bien qu'un hérite de l'autre).

B. Non, car si on choisit `ArrayList`, c'est pour bénéficier des complexités algorithmiques favorables à ce qu'on cherche à faire (par exemple la méthode `get(i)` qui tourne en temps constant). Substituer le type déclaré par `List` nous enlèverait ces avantages.

C. Non, puisque si les variables `list` sont déclarées comme `List`, nous perdons accès à toutes les méthodes de `ArrayList`.

D. Non, les deux options sont complètement équivalentes et il n'y a aucun avantage à substituer `ArrayList` par `List`.

E. Oui, déclarer le type le plus général possible est une bonne pratique, car elle garantit le minimum de changements le jour où l'on décide de substituer une implémentation par une autre.
***

### Solution


Puisque la classe `ArrayList` hérite de l'interface `List`, il est tout à fait raisonnable de "traiter" une `ArrayList` comme une `List`, il s'agit d'un principe de base d'héritage en Java. La réponse `A` n'a donc pas de sens.

Peu importe si le type **déclaré** change, le type instancié restera le même. Il n'y a donc aucune perte de performances même si `ArrayList` n'est pas directement déclaré. L'argument qu'enforcer une sous-classe particulière permet d'éviter que l'utilisateur fournisse une autre implémentation moins efficace pour la tâche pourrait éventuellement justifier la réponse **B**, mais dans ce cas tout ce que `print` fait est d'afficher les éléments de la liste via un itérateur, et il n'y a pas vraiment d'implémentation plus rapide qu'une autre pour cette tâche.

Toutes les méthodes "intéressantes" concernant les listes sont directement présentes dans l'interface `List`, et `ArrayList` ne fait que les implémenter sans en ajouter d'autres. Il n'y donc aucune perte d'accès aux méthodes.

Déclarer le type le plus général est souvent une bonne chose, et ce pour plusieurs raisons:

- Cela rend le code plus simple à comprendre, et plus prévisible. Imaginez une classe `Human` et une interface `CanBreathe` implémentée par `Human`. une méthode `blow` qui prendrait en paramètre un `Human` est moins prévisible que si elle demandait un `CanBreathe`: dans le premier cas elle a le "pouvoir" de faire tout ce qui est possible de faire avec un humain, malgré le fait qu'elle ne devrait être capable d'interagir qu'avec la partie "respiratoire" d'un humain.
- Cela rend le code plus général, plus accessible. Si dans le futur vous avez d'autres classes implémentant `CanBreathe`, vous pourrez utiliser la méthode `blow` sans avoir à la changer, malgré le fait qu'elle était initialement destinée à des humains. 
Un petit article avec plus de détails sur le sujet est disponible [ici](https://github.com/readthedocs-fr/notions/blob/master/prog_orientee_objet/abstraction/fr/ABSTRACTION.md).

La réponse correcte est donc la réponse **E**
