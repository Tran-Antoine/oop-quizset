---
layout: page
title:  "Lecture de code 2"
---

Soit l'interface `Mix` définie ci-dessous.
```java
public interface Mix<T> {

    public interface Mapper<A, B> {
        B apply(A a);
    }

    default <S> Mix<S> map(Mapper<Mix<T>, Mix<S>> mapper) {
        return mapper.apply(this);
    }

    default <U, S> U consume(Mapper<Mix<T>, Mix<S>> mapper, Mapper<S, U> consumer) {
        return consumer.apply(this.map(mapper));
    } 
}
```

Vrai ou Faux: 

Tout le code lié au génériques (paramètres génériques, variables génériques, etc) est correct (d'un point de vue syntaxique), et le code compile donc sans erreur.


***

### Solution

Résumons ce que les deux méthodes proposent.

- `map` permet de passer d'un `Mix<T>` (this) à un `Mix<S>`, à l'aide d'une fonction mapper `Mix<T> => Mix<S>`
- consume permet de passer d'un `Mix<T>` (this) à un `U`, à l'aide d'une fonction mapper `T => S` et `S => U`

La méthode `map` ne pose pas de problème particulier, la fonction `apply` en question demande un `Mix<T>` et `this` est fourni, ce qui est valide. Elle renvoie un `Mix<S>`, qui est bien le type de retour de la fonction `map`.

En revanche, la fonction `consume` est problématique: bien que l'appel à `map` soit correct pour la raison citée au-dessus, le type de retour de `map` est `Mix<S>`. Mais `consumer` demande un `S` en paramètre de `apply`, et non un `Mix<S>` ! Le code ne compile donc pas.

La réponse correcte est donc **Faux**.
