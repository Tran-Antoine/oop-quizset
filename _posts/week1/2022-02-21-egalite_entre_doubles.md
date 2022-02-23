---
layout: page
title:  "Egalité entre doubles"
---

Vrai ou Faux:
Le programme suivant est une bonne manière de vérifier que la méthode `foo` fonctionne, du moins partiellement.
Partez du principe que `foo` est une procédure quelconque, et que `foo(a, b)` devrait être égal à `expected`.

```java
@Test
void method_foo_works() {

	double a = 7.823;
	double b = 2;
	
	double result = foo(a, b);
	double expected = 27.894;
	
	assertEquals(expected, result);

}
```


***

### Solution

Tester l'égalité entre deux `doubles` n'est jamais une bonne idée étant donné que même si les valeurs peuvent sembler égales en ne regardant que quelques chiffres significatifs, 
elles ne seront jamais exactement les mêmes. Dans ce genre de cas il vaut mieux utiliser une variante de la méthode `assertEquals` dont l'entête est la suivante : `assertEquals(double expected, double actual, double delta)`.
L'argument `delta` est la tolérance et le test ne passe que si la différence entre `expected` et `actual` est plus petite que `delta`.  

Il en suit donc que la réponse correcte est **Faux**