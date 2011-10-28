[XKE] Hands On : Programmation fonctionnelle
============================================

### Préliminaire

Créer un projet maven et récupérer le pom.xml de ce repo Github.

- groupId: xke-fp
- artifactId: xke-fp
- version: 1.0

Pour les assertions, ...

***

### Hands On 1 : Fonction récursive en Guava

Programmer une version de la fonction factorielle en se basant sur Guava.

Tests unitaires

    fact(0) = 1
    fact(1) = 1
    
    fact(5) = 120
    
    fact(10) = 3628800

***

### Hands On 2 : Filter

On fournit une liste de salaires. Ecrire la méthode `HandsOn.lessThan()` qui ne conserver
les salaires inférieurs strictement à 3000 en utilisant `Iterables.filter()`.

    List<Double> salaries = Arrays.asList(1000.0, 2000.0, 2500.0, 3000.0, 4000.0);
    List<Double> newSalaries = HandsOn.lessThan(3000.0, salaries);
    assertThat(newSalaries).containsExactly(1000.0, 2000.0, 2500.0);

***

### Hands On 3 : Map / Transform

Ecrire la méthode `HandsOn.increaseSalaries()` qui applique une augmentation identique à
une liste de salaires en utilisant `Iterables.transform()` (équivalent de `map` en Guava).

    List<Double> salaries = Arrays.asList(1000.0, 2000.0, 2500.0, 3000.0, 4000.0);
    List<Double> newSalaries = HandsOn.increaseSalaries(salaries, 0.02);
    assertThat(newSalaries).containsExactly(1020.0, 2040.0, 2550.0, 3060.0, 4080.0);

***

### Hands On 4 : Fold / Reduce

La fonction `fold()` n'existe pas en Guava. Ecrire la fonction `fold()` et utiliser cette
fonction pour calculer une somme de nombres.

    // signature
    <T, R> R fold(Iterable<T> values, R init, Function<R, Function<T, R>> function)
    
    // test unitaire
    List<Integer> values = Arrays.asList(1, 2, 3);
    Integer result = HandsOn.fold(values, 0, sum);
    assertThat(result).isEqualTo(6);
