[XKE] Hands On : Programmation fonctionnelle
============================================

### Préliminaire

Créer un projet maven et récupérer le pom.xml de ce repo Github.

- groupId: xke-fp
- artifactId: xke-fp
- version: 1.0

La doc de Guava est ici : http://docs.guava-libraries.googlecode.com/git-history/v10.0.1/javadoc/

Pour les assertions, Fest-assert est utilisé : http://docs.codehaus.org/display/FEST/Fluent+Assertions+Module
L'utilisation optimale de cette API nécessite d'intégrer l'import static suivant :

    import static org.fest.assertions.Assertions.assertThat;

La présentation est disponible à l'adresse :
https://docs.google.com/presentation/d/19iWQ4d_05Ahsc24p3JgpFoKalUbt-RNK3XQMv0ZdEUA/edit

***

### Hands On 1 : Fonction récursive

Programmer une version de la fonction factorielle.

    // test unitaire
    fact(0) = 1
    fact(1) = 1
    
    fact(5) = 120
    
    fact(10) = 3628800

Réaliser cette exercice en Java seulement puis en utilisant l'interface Function de Guava,
dans sa forme récursive simple puis dans sa forme récursive terminale.

***

### Hands On 2 : Filter

On fournit une liste de salaires. Ecrire la méthode `HandsOn.lessThan()` qui ne conserver
les salaires inférieurs strictement à 3000 en utilisant `Iterables.filter()`.

    // test unitaire
    Iterable<Double> salaries = Arrays.asList(1000.0, 2000.0, 2500.0, 3000.0, 4000.0);
    Iterable<Double> newSalaries = HandsOn.lessThan(3000.0, salaries);
    assertThat(newSalaries).containsOnly(1000.0, 2000.0, 2500.0);

***

### Hands On 3 : Map / Transform

On fournit une liste de salaires.
Ecrire la méthode `HandsOn.increaseSalaries()` qui applique une augmentation identique à
une liste de salaires en utilisant `Iterables.transform()` (équivalent de `map` en Guava).

    // test unitaire
    Iterable<Double> salaries = Arrays.asList(1000.0, 2000.0, 2500.0, 3000.0, 4000.0);
    Iterable<Double> newSalaries = HandsOn.increaseSalaries(salaries, 0.02);
    assertThat(newSalaries).containsOnly(1020.0, 2040.0, 2550.0, 3060.0, 4080.0);

***

### Hands On 4 : Fold / Reduce

La fonction `fold(list, init, function)` n'existe pas en Guava. Ecrire la fonction `fold()` et utiliser cette
fonction pour calculer une somme de nombres.

    // signature
    // <T, R> R fold(Iterable<T> values, R init, Function<R, Function<T, R>> function)
    
    // test unitaire
    List<Integer> values = Arrays.asList(1, 2, 3);
    Integer result = HandsOn.fold(values, 0, sum);
    assertThat(result).isEqualTo(6);

***

### Hands On 5 : Zip

Écrire la fonction `HandsOn.zipWith(function, list1, list2)` qui fusionne deux listes en se
basant sur une fonction.

    // signature
    // <T1, T2, R> Iterable<R> zipWith(Function<T1, Function<T2, R>> function, Iterable<T1> list1, Iterable<T2> list2)
    
    // test unitaire
    Iterable<Integer> result = zipWith(sum, Arrays.asList(1, 2), Arrays.asList(3, 4, 6));
    assertThat(result).containsExactly(4, 6);

***

### Hands On 6 : Liste d'entiers infinis avec Guava

Écrire la méthode `HandsOn.enumPositiveInts()` qui retourne un `Iterable<Integer>` contenant
tous les entiers à partir de 0 jusqu'à _l'infini_. Vous écrirez cette méthode est utilisant
la classe `AbstractIterator` mise à disposition par Guava.

    // test unitaire
    Iterable<Integer> fiveInts = Iterables.limit(HandsOn.enumPositiveInts(), 5);
    assertThat(fiveInts).containsExactly(0, 1, 2, 3, 4);

    Iterable<Integer> fiveNextInts = Iterables.limit(Iterables.skip(HandsOn.enumPositiveInts(), 5), 5);
    assertThat(fiveInts).containsExactly(5, 6, 7, 8, 9);

***

### Hands On 7 : Fibonnacci sous forme de liste infinie

Écrire la fonction `HandsOn.fibs()` qui retourne une liste infinie contenant la suite de Fibonnacci.

    // test unitaire
    assertThat(Iterable.limit(HandsOn.fibs(), 8)).containsExactly(0, 1, 1, 2, 3, 5, 8, 13);
