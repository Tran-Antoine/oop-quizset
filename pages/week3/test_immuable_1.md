---
layout: page
title:  "Test d'immuabilité 1"
---

Vrai ou Faux: 

La classe suivante est immuable.
```java
public final class Cours {
    
    private final List<String> eleves;

    public Cours(List<String> eleves) {
        this.eleves = List.copyOf(eleves);
    }

    public List<String> getEleves() {
        return eleves;
    }
}
```

***

### Solution

* La classe `Cours` est déclarée `final`
* Ses attributs sont déclarés `final`
* `eleves` est une liste de `String`, qui est une classe immuable
* `eleves` est copiée **et** la copie est rendue immuable dans le constructeur (grâce à `copyOf`)

Il n'y a aucune manière de modifier une quelconque instance de la classe `Cours`. La réponse correcte est donc **Vrai**