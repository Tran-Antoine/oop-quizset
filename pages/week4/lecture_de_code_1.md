---
layout: page
title:  "Lecture de code 1"
---

> ⚠️ Vous n'avez **pas** besoin de comprendre en détail ce que fait le code présenté ! Tout ce qui est demandé est une analyse de l'utilisation des génériques.

Soit la classe `ProbabilityLaw` définie ci-dessous.
```java
public class ProbabilityLaw<T> {

    private final List<Pair<T, Float>> events;
    private final Random random;
    private float totalWeight;

    public ProbabilityLaw() {
        this.events = new ArrayList<>();
        this.random = new Random();
        this.totalWeight = 0;
    }

    public void add(T element, float weight) {
        // 0 weight elements are not taken into account
        if(weight == 0) return;

        events.add(new Pair<>(element, weight));
        totalWeight += weight;
    }

    public void clear() {
        events.clear();
        totalWeight = 0;
    }

    public void remove(T element) {
        Pair<T, Float> toRemove = null;

        for(Pair<T, Float> pair : events) {
            if(pair.k.equals(element)) {
                toRemove = pair;
            }
        }

        if(toRemove != null) {
            totalWeight -= toRemove.v;
            events.remove(toRemove);
        }
    }

    public T draw() {
        if(events.size() == 0) {
            throw new IllegalStateException("No element to be drawn");
        }

        float current = 0;
        float randValue = random.nextFloat() * totalWeight;
        T previous = null;

        for(Pair<T, Float> event : events) {
            float value = event.v;
            T key = event.k;
            if(current > randValue) {
                return previous;
            }
            previous = key;
            current += value;
        }
        return previous;
    }

    private static class Pair<K, V> {

        private final K k;
        private final V v;

        private Pair(K k, V v) {
            this.k = k;
            this.v = v;
        }
    }
}
```

Vrai ou Faux: 

Tout le code lié aux génériques (paramètres génériques, variables génériques, etc) est correct (d'un point de vue syntaxique), et le code compile donc sans erreur. Partez du principe que tout code non lié à la généricité est correct.


***

### Solution

En établissant la liste des utilisations de la généricité:

- On donne à `ProbabilityLaw` un type générique `T` quelconque
- On définit une liste de paires, de type `T` et `Float` respectivement
- L'ajout d'un élément ajoute bien une nouvelle instance de `Pair` avec paramètres `T` et `float`, qui correspondent bien à une `Pair<T, Float>`
- Parcourir la liste `events` nous donne bien des `Pair<T, Float>`
- `pair.k` est bien de type `T`, donc utiliser `equals` sur le paramètre de type `T` a du sens
- `toRemove.v` est bien de type `Float`, cela a donc du sens de décrémenter la valeur `totalWeight` qui est aussi de type `float`
- Le principe est le même pour la méthode `draw`

La réponse correcte est donc **Vrai**.

***

### Pour aller plus loin

Afin de simplifier la question, une liste de `Pair` a été utilisée. Si cela vous intéresse, il existe une collection en java bien plus pratique pour ce genre d'opérations, appelée `HashMap`. Cette classe sera vue en détail plus tard dans le semestre, mais elle permet (entre autres) de lier une "clé" à une "valeur", en s'assurant qu'il ne peut pas exister deux fois la même clé.
