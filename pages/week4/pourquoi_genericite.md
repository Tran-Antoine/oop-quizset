---
layout: page
title:  "Remplacer la généricité"
---

Les deux codes suivants sont-ils équivalents ? Pourquoi ?

```java
public class Group<A> {

    private List<A> list = new ArrayList<>();

    public void add(A element) {
        this.list.add(element);
    }

    public A get(int index) {
        return this.list.get(index);
    }
}
```
```java
public class Group {

    private List<Object> list = new ArrayList<>();

    public <A> void add(A element) {
        this.list.add(element);
    }

    public <A> A get(int index) {
        return (A) this.list.get(index);
    }
}
```

A. Oui, car ils permettent dans les deux cas d'ajouter un élément d'un certain type et de récupérer un élément du même type

B. Oui, car comme `A` n'est pas borné, il peut être de n'importe quel type, et il est donc équivalent de simplement travailler avec des `Object`, vu que toute classe hérite de `Object`.

C. Non, car `list` étant une liste d'`Object`, il est impossible de lui ajouter des éléments de type `A`

D. Non, car les deux types `A` de `add` et `get` ne sont pas fixés, il est donc possible d'ajouter un élément d'un certain type et de demander à en récupérer un d'un type différent.

***

### Solution

La proposition `C` n'a pas de sens: il est tout à fait possible d'ajouter des éléments de n'importe quel type dans la liste, puisqu'il s'agit d'une liste d'`Object`, et ce quel que soit `A`.

Il est essentiel de remarquer que malgré que dans le second code, malgré que les deux génériques aient le même nom `A`, ils ne sont en aucun cas liés. De manière similaire, dans le code suivant:
```java
void foo() {
    int test = 0;
    (...)
}

void bar() {
    int test = 1;
    (...)
}
```
les deux variables `test` n'ont aucun lien entre elles, bien qu'elles aient le même nom. Elle ne sont pas dans le même **scope**. C'est le même principe pour les paramètres génériques `A`. De plus, ces derniers ne sont pas fixes ! A chaque appel de `add`, l'utilisateur choisit implicitement ou explicitement le type `A`, et l'objet donné en paramètre est ajouté. A chaque appel de `get`, l'utilisateur **choisit** également implicitement ou explicitement le type qu'il veut récupérer, et la méthode `get` force un transtypage pour lui donner ce qu'il veut. Mais cela peut mener à bien des erreurs ! Par exemple, ce code compile parfaitement bien:
```java
Group group = new Group();
group.add("Hello");
Integer value = group.get(0);
```
puisque l'utilisateur a le contrôle complet du type `A`. Pourtant, il y aura une erreur de transtypage pendant l'exécution.

En revanche, le premier code fixe pour de bon à l'instanciation (selon le choix de l'utilisateur) le type générique `A`, il est donc commun et constant à la fois pour `add` et `get`, ce qui nous assure qu'il n'y aura pas d'erreur de transtypage.

La réponse correcte est donc la réponse **D**.

