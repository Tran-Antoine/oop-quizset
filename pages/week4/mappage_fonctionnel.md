---
layout: page
title:  "Mappage fonctionnel"
---

Soit l'interface `Opener` définie ci-dessous.

```java
public interface Opener<P, R> {

    R open(P tool);

}
```

On cherche à écrire une fonction `mapList`, qui prend en paramètre une `List<Pokeball>` et un `Opener<???>`, et renvoie une `List<Pokemon>`, qu'elle calcule en créant une nouvelle liste, et en "convertissant" chaque pokeball en un pokémon à l'aide de la fonction `open` de l'objet `Opener`. 

> ⚠️ Compléter les `???` n'est pas une tâche triviale, et cette question ne vous demande pas de savoir le faire. 

La raison pour laquelle les types `P` et `R` ne sont pas bornés par `Pokeball` et `Pokemon` respectivement est qu'il est possible d'utiliser des openers pour autre chose que des pokémons, des boîtes de tomates en conserve par exemple.

Quels types d'Opener devraient logiquement être acceptés par la fonction `mapList` ? Choisissez la réponse la plus précise.

> Note: considérez que `PikachuBall` hérite de `Pokeball`, que `Pikachu` hérite de `Pokemon`, etc. De plus, dû à un évènement spécial, il est techniquement possible d'obtenir un pokémon rare peu importe la pokeball utilisée. Par exemple, un `DenticrisseBall` peut potentiellement produire un `Rayquaza`.


A. `Opener<Pokeball, Pokemon>`

B. `Opener<PikachuBall, Pokemon>`

C. `Opener<Pokeball, Dracaufeu>`

D. `Opener<PikachuBall, Dracaufeu>`

E. Les types `A` et `B`

F. Les types `C` et `D`

G. Les types `A` et `C`

H. Tous les types ci-dessus.

***

### Solution

Etant donné que nous recevons une liste de `Pokeball` en paramètre sans aucune information supplémentaire, il est important de noter que le type fourni en paramètre de `open` sera toujours `Pokeball` et jamais un type "plus précis".

Ainsi, les réponses `B` et `D` sont impossibles, puisqu'il s'agit de "convertisseurs" qui **nécessitent** des `PikachuBall`, et malheureusement nous n'avons pas plus précis que `Pokeball`.

Il semble plutôt évident que la `A` est correcte: elle demande des `Pokeball` (qui peuvent être fournies depuis la liste) et les transforme en `Pokemon` de n'importe quel type.

En revanche, la réponse `C` est également correcte ! La méthode doit renvoyer une `List<Pokemon>`, et il est tout à fait possible d'ajouter des pokémons de type `Dracaufeau` dedans, quitte à ce que tous les pokémons ajoutés soient des dracaufeus.

La réponse correcte est donc la réponse `G`.

***

### Pour aller plus loin

Une question qui n'a pas été résolue est: quel type exact d'Opener faudrait-il demander en paramètre de la fonction `mapList` ? `Opener<Pokeball, Pokemon>` serait bien trop restrictif, car il n'accepterait pas les `Opener<Pokeball, Dracaufeu>` par exemple. Concrètement, ils nous faut demander un opener qui:

- Accepte en paramètre n'importe quel objet de type `Pokeball` (ou plus précis)
- Renvoie n'importe quel objet de type `Pokemon` (ou plus précis)

Ainsi, le premier type générique correspondant au paramètre de `open` doit être "n'importe quelle classe **mère** de `Pokeball` (`Pokeball` inclue)", puisque s'il sera donc possible de lui donner une `Pokeball`. Le deuxième type générique correspondant au retour de `open` doit être "n'importe quelle classe **fille** de `Pokemon` (`Pokemon` inclue)", puisqu'il sera possible de considérer ce type de retour comme un objet de type `Pokemon`. La sytaxe pour ce faire est la suivante:

```java
public List<Pokemon> mapList(List<Pokeball> list, Opener<? super Pokeball, ? extends Pokemon> opener) { ... }
```