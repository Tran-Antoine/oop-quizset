---
layout: page
title:  "Affirmations sur l'immuabilité"
---

Quelle proposition est **incorrecte** à propos de l'immuabilité ?

A. Il n'est en principe **jamais** utile de copier une instance d'une classe immuable.

B. Si on parle d'une liste (déclarée `final`) d'objets qui sont **immuables**, alors liste immuable et liste non-modifiable sont synonymes.

C. Un inconvénient de l'immuabilité est que certains programmes peuvent être plus lents, en raison du besoin de créer des objets plus souvent.

D. Une classe immuable **peut** contenir des attributs muables, tant qu'ils ne sont jamais modifiés à l'intérieur, et qu'ils sont copiés / rendus non modifiables avant d'être fournis à l'extérieur. 

***

### Solution

Puis que les objets muables ne peuvent jamais être modifiés, partager une même entre différentes parties du programme ne pose aucun problème. De ce fait, l'existence de deux objets "équivalents" mais non identiques n'a aucun intérêt: la copie n'a donc aucun intérêt non plus.

Que l'attribut soit `final` ou pas, cela n'a aucun impact sur le fait qu'une liste immuable et une liste non-modifiable ne sont pas la même chose. Le fait que les objets contenus dans ladite liste soient immuables n'a aucun impact non plus: cela n'empêche pas d'ajouter ou supprimer des éléments de cette dernière.

Selon la définition du cours, posséder des attributs muables n'est en soi pas une atteinte à l'immuabilité, tant qu'une grande prudence est exercée lorsqu'il s'agit d'utiliser / partager ces attributs.

La création répétée d'instances afin d'éviter la muabilité pouvant en effet nuire aux performances, il s'ensuit que la réponse correcte est la réponse **B**
