---
layout: page
title:  "Test d'immuabilité 3"
---

Vrai ou Faux:

La classe `Cours` est immuable.
> Note: le constructeur de la classe `Cours` étant privé et le code donné étant exhaustif, seul `CoursBuilder` peut l'instancier.
```java

public final class Cours {

    private final List<String> names;

    private Cours(List<String> names) {
        this.names = names;
    }

    public void faireAppel() {
        for (String s : names) {
            System.out.println(s + "?");
        }
    }

    public static final class CoursBuilder {
        private List<String> list;
        public CoursBuilder() {
            this.list = new ArrayList<>();
        }
        public CoursBuilder add(String s) {
            list.add(s);
            return this;
        }
        public CoursBuilder clear() {
            list.clear();
            return this;
        }
        public Cours build() {
            return new Cours(list);
        }
    }
}
```

***

### Solution

Question tirée d'une perte de points personnelle dans le projet de `2021` 😄

A première vue, puisque seul le `CoursBuilder` a accès au constructeur de `Cours`, et que c'est lui qui initialise la liste, il semble qu'une copie de `names` dans le constructeur de `Cours` est inutile. Mais ce contre-exemple pernicieux prouve le contraire:
```java
CoursBuilder builder = new CoursBuilder();
Cours cours = builder
    .add("Antoine")
    .add("Alban")
    .add("Michel")
    .build();

cours.faireAppel(); // Affiche Antoine, Alban et Michel
builder.clear();
cours.faireAppel(); // n'affiche rien
```

Il s'ensuit donc que la réponse correcte est **Faux**