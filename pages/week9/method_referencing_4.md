---
layout: page
title:  "Référence de méthode 4"
---

On définit la classe `Student` ci-dessous:
```java

public class Student {

    private final String name;

    public Student(String name) {
        this.name = name;
    }

    public String help(Student other) {
        return this.name + " a aidé " + other.name;
    }
}
```
Qu'affiche le programme suivant ?

```java

Student s1 = new Student("Alban");
Student s2 = new Student("Antoine");

// BiFunction permet de représenter une fonction à deux arguments, ici une fonction (Student, Student) => String
BiFunction<Student, Student, String> combiner = Student::help; 

// apply "applique" la fonction aux arguments donnés et retourne le résultat
System.out.println(combiner.apply(s1, s2));

```

A. Le programme ne compile pas

B. Alban a aidé Antoine

C. Antoine a aidé Alban

D. Antoine a aidé Antoine

E. Alban a aidé Alban

***

### Solution


Il s'agit d'une utilisation particulière du référençage de méthode. Il est important de noter que la fonction `help` ne prend qu'un seul argument en paramètre, alors qu'on l'attribue comme valeur de fonction qui prend deux paramètres (deux fois `Student`). Malgré tout, le code compile ! Bien qu'un seul paramètre soit nécessaire à la méthode `help`, il est crucial de remarquer que cette méthode n'est **pas** statique, elle dépend donc d'une instance de type `Student`. Pour pouvoir appeler la fonction `help`, nous avons donc besoin de:
- Un étudiant sur lequel appeler la méthode
- Un étudiant à passer en paramètre

Dans ce cas de figure, l'ordre appliqué est **toujours** le même:
- Le premier paramètre correspond à "sur qui on appelle la méthode"
- Le deuxième paramètre correspond à "qui on passe en paramètre de la méthode appelée"

La réponse correcte est donc la réponse **B**
