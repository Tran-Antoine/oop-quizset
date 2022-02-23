---
layout: page
title:  "Lecture de code 4"
---

Quel morceau de code teste la méthode `duplicate` décrite ci-dessous avec le plus de fiabilité ?
Lorsque nécessaire, partez du principe que `someRandomArrayOfInts` renvoie un tableau de taille aléatoire contenant des entiers aléatoires.
> Note: la fonction `duplicate` présentée est correctement implémentée, mais partez du principe que vous testez une fonction dont vous ne connaissez pas la validité. 

```java
public int[] duplicate(int[] in) {
	int[] out = new int[in.length * 2];
	int i = 0;
	while (i < out.length) {
		int val = in[i/2];
		out[i++] = val;
		out[i++] = val;
	}
	
	return out;
}
```

A.
```java
for(int n = 0; n < 200; n++) {
	int[] in = someRandomArrayOfInts();
	int[] out = duplicate(in); 

	assertEquals(2*in.length, out.length);
	for(int i = 0; i < out.length; i++) {
		if(i % 2 != 0) {
			assertEquals(out[i-1], out[i]);
		}
	}
}
```

B.
```java
int[] in = {1, 2, 3};
int[] out = duplicate(in);
assertEquals(new int[]{1, 1, 2, 2, 3, 3}, out);
```

C.
```java
for(int n = 0; n < 200; n++) {
	int[] in = someRandomArrayOfInts();
	int[] out = duplicate(in);
	assertEquals(2*in.length, out.length);
	for(int i = 0; i < in.length; i++) {
		assertEquals(in[i], out[2*i]);
		assertEquals(in[i], out[2*i + 1]);
	}
}
```

***

### Solution

De toute évidence, la réponse B n'est pas une façon très fiable de vérifier notre méthode `duplicate`: elle pourrait toujours renvoyer le même tableau `{1, 1, 2, 2, 3, 3}` sans tenir compte du paramètre, et le test passerait tout de même.

La proposition A pose un problème un peu plus subtil: malgré que la taille du tableau résultat soit vérifiée, et que le fait que tous les éléments sont doublés est également vérifié, il n'y a aucun réel test du contenu du résultat par rapport à l'input. Par exemple, `duplicate` pourrait renvoyer un tableau de taille `2*in.length`ne contenant que des zéros, et le test passerait.

La proposition C, quant à elle, compare bien le contenu du résultat avec le tableau passé en entrée.

La réponse correcte est donc la réponse **C**