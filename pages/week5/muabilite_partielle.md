---
layout: page
title:  "Muabilité partielle des vues"
---

De manière générale, une collection est toujours soit complètement modifiable (aucune méthode ne lance d'exception `UnsupportedOperationException`) ou complètement non-modifiable (toutes les méthodes de modification lancent des exceptions).
Cependant, certaines collections / vues échappent à la règle, dont **une ou plusieurs** parmi celles ci-dessous. Laquelle/Lesquelles ?

> Indice: Partez du principe que ces vues *souhaiteraient* être muables: si une opération n'est pas supportée pour une d'entre elles, c'est forcément parce que l'opération poserait un problème.
 
A. `Arrays.asList(new int[]{5, 8, 3})`

B. `new ArrayList<>(List.of(1, 7, 9, 56)).subList(0, 2)` 

C. `new HashMap<>().keySet()`

D. `new HashMap<>().values()`

***

### Solution

Il est important de noter que tous les objets ci-dessus sont des **vues**, et qu'ils sont donc, en un sens, *liés* à la collection qu'ils décrivent. Les restrictions de cette collection d'origine est la raison qui explique pourquoi certaines opérations ne peuvent pas être supportées, malgré la volonté de rendre les vues muables.

La réponse **A** propose une vue de type `List`sur un **tableau**. Or, il est bien connu qu'un tableau est de taille fixe: la méthode `add` ne peut donc pas être supportée par la vue ! En revanche, il n'y a aucun problème à utiliser la méthode `set`.

La réponse **B** propose une vue de type `List` sur une liste, plus précisément sur une portion de la liste. Il n'y a pas de raison qui empêche l'ajout d'éléments dans cette vue, la suppression ou la modification.

La réponse **C** propose une vue de type `Set` sur une map. Bien qu'il soit logique que l'opération `remove` soit supportée (qui supprimerait également la paire clé/valeur dont la clé correspond à la valeur retirée), la méthode `add` ne peut pas vraiment l'être: il faudrait également ajouter une nouvelle clé dans la map, mais il est impossible de déterminer de manière logique quelle valeur lui serait associée !

La réponse **D** fait face au même problème: retirer une valeur de la vue retirerait également une paire clé/valeur de la map dont la valeur correspondrait à la valeur retirée, en revanche l'ajout d'une nouvelle valeur dans la vue serait problématique: il est impossible de déterminer la clé qui lui correspondrait dans la map.

Les réponses correctes sont donc les réponses **A**, **C**, et **D**.
