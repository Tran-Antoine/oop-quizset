---
layout: page
title:  "Pourquoi écrit-on des tests unitaires ?"
---

Quelle proposition concernant les tests unitaires est la plus correcte ?

A. Les tests unitaires garantissent qu'un composant du programme fonctionne. 
Si on teste tous les composants, on peut donc avoir la garantie que le programme entier fonctionne.

B. Les tests unitaires sont utiles pour trouver des bugs dans le code. 
En revanche, même avec du *testing* en profondeur, nous n'avons pas la garantie que le programme fonctionne parfaitement.

C. Les tests unitaires permettent de remplacer les *reviews* de code lorsqu'on code en groupe. 
Quand quelqu'un souhaite ajouter du code au programme, il suffit de bien regarder les tests écrits pour valider (ou non) le code.

D. Il est toujours facile de tester des composants. 
Si un certain bout de code est trop compliqué à tester, il suffit de le découper en petits blocs et de tester chaque bloc séparément.

### Solution

Cette question a pour but de vérifier le rôle que les tests jouent dans un programme. Cela peut paraître contre-intuitif, mais dans un sens, les tests ne servent pas à vérifier la validité du programme, ils servent à **trouver des problèmes**. Lorsqu'un test (correctement écrit) échoue, on a la garantie qu'une partie de notre code ne fonctionne pas. En revanche, la réciproque est fausse: il est tout à fait possible que certains problèmes dans le code passent inaperçus dans les tests !

De plus, les tests unitaires jouent un rôle uniquement dans l'aspect **fonctionalité** du programme. Ils ne vérifient pas si un code est proprement écrit, flexible, efficace, etc. Ils ne peuvent donc en aucun cas complètement remplacer les *reviews* de code. 

Malheureusement, il est parfois difficile de mettre en place des tests unitaires pour certains composants du programme. Par exemple, il est très difficile de vérifier qu'une interface graphique est fonctionnelle.

La réponse correcte est donc la réponse **B**.