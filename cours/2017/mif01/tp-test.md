---
layout: page
title: Mif01 - TP Introduction  à  JUnit
permalink: /cours/2017/mif01/tp-test.html
---

[Revenir a la page du cours](.)

Par Emmanuel Coquery, Marie Lefevre, Lionel Médini et Aurélien Tabard, màj le 19/09/2016

## Préambule
Ce TP se fait en binôme. Le code est à rendre à la fin de la séance.
Mettre le projet sur la forge avec Lionel Medini et Aurélien Tabard en reporter, et renseigner [ce formulaire spiral](http://spiralconnect.univ-lyon1.fr/webapp/assessment/assessmentAnswer.html?id=6031890&mode=answer).

## Découverte de JUnit
JUnit est un framework de tests unitaire pour Java créé par Kent Beck et Erich Gamma. Il permet de simplifier
considérablement l’écriture des tests en offrant un ensemble d’outils. Il permet notamment d’écrire des jeux de tests
facilement réutilisables, et de regrouper les tests en fonction des besoins, des objets, etc. JUnit est aussi un framework
extensible : par exemple, DBUnit propose des outils supplémentaires pour les tests spécifiques aux bases de données.
Utiliser des tests unitaires permet non seulement de tester un programme et donc d’en assurer la qualité, mais
également d’éviter les régressions dans le code. Avec JUnit, on définit des tests réutilisables que l’on peut exécuter à
volonté. Lorsque le code a progressé, on peut relancer une série de tests. Si les tests se passent toujours bien, alors
on peut considérer que le code n’a pas régressé.
Un des intérêts de JUnit est qu’il permet d’écrire les tests avant le code. En procédant ainsi, au début, le programme
n’est pas livrable car il ne passe aucun test. Plus le code progresse et plus le nombre de tests passés augmente.


> La version actuelle de JUnit est la version 4. JUnit 4 s'appuie sur les annotations, à la différence des versions précédentes. Lorsque vous réaliserez les exercices de ce TP, faites bien attention à la version de JUnit que vous utilisez, et au code que vous copiez/collez.

> JUnit est le framework le plus utilisé pour les tests unitaires en Java, mais il n’est pas le seul !

Pour la plupart des langages de programmation, il existe de framework xUnit ou équivalent :  

  - CUnit pour C ;
  - cppunit, GoogleTest, BoostTest pour C++ ;
  - JUnit et TestNG pour Java ;
  - JSUnit pour JavaScript ;
  - PHPUnit et SimpleTest pour PHP ;
  - ...

Références utiles pour le TP et sources :

 - http://www.junit.org/
 - https://github.com/KentBeck/junit/downloads

## Exercices

### Mettre en place des tests unitaires avec Netbeans ou Eclipse

Suivez le tutoriel disponible à cette adresse : http://netbeans.org/kb/docs/java/junit-intro.html pour Netbeans; ou ici: https://courses.cs.washington.edu/courses/cse143/11wi/eclipse-tutorial/junit.shtml pour Eclipse.

> Il ne s'agit pas de suivre tout le tutoriel mais de mettre en place un projet permettant d'utiliser JUnit.


####  Démarrage avec JUnit
Dans cet exercice, nous allons chercher à comprendre un premier exemple de code utilisant la librairie JUnit.
Observez le code suivant.

~~~~~~~~
import junit.framework.*;
public class SimpleTest extends TestCase {
  public SimpleTest(String name) {
    super(name) ;
  }
  public void testSimpleTest () {
    int answer = 2; assertEquals((1+1), answer);
  }
}
~~~~~~~~
<!-- {: .language-java} -->

  - Créez une classe SimpleTest.java contenant le code présenté ci-dessus.
  - Au besoin, adaptez cette classe pour la rendre conforme au mode de fonctionnement de JUnit4.
  - Exécutez le test.
  - Introduisez une erreur dans votre classe (par exemple, en changeant la valeur de la variable answer) et relancez le test.
Que se passe-t-il ?



#### Externalisation des tests
Dans cet exercice, nous allons voir comment définir une classe test qui regroupe plusieurs tests. Voici le code de la classe à tester.

~~~~~~~~
// A Class that adds up a string based on the ASCII values of its
// characters and then returns the binary representation of the sum.
public class BinString {

  public BinString () {}

  public String convert(String s) {
    return binarise(sum(s));
  }

  public int sum(String s) { if (s=="") return 0;
    if(s.length()==1)
      return ((int)(s.charAt(0)));

    return ((int)(s.charAt(0)))+sum(s.substring(1));
  }

  public String binarise(int x) {
    if (x==0) return "";
    if(x%2==1) return "1"+binarise(x/2);
    return "0"+binarise(x/2);
  }
}
~~~~~~~~

Voici maintenant le code de la classe test.

~~~~~~~~
import junit.framework.*;

public class BinStringTest extends TestCase {

  private BinString binString;

  public BinStringTest(String name) {
    super (name);
  }

  protected void setUp() {
    binString = new BinString ();
  }

  public void testSumFunction () {
    int expected = 0;
    assertEquals(expected, binString.sum(""));
    expected = 100;
    assertEquals(expected, binString.sum("d"));
    expected = 265;
    assertEquals(expected , binString.sum("Add"));
  }

  public void testBinariseFunction () {
    String expected = "101";
    assertEquals(expected, binString.binarise(5));
    expected = "11111100";
    assertEquals(expected, binString.binarise(252));
  }

  public void testTotalConversion () {
    String expected = "1000001";
    assertEquals(expected, binString.convert("A"));
  }
~~~~~~~~

  - En vous aidant de la javadoc de Junit, cherchez ce que fait la classe BinStringTest.
  - Adaptez la classe test pour la faire fonctionner avec JUnit 4.
  - Lancez les tests.
  - En vous aidant des résultats des tests, corrigez les erreurs dans la classe principale.
  - Relancez les tests jusqu’à ce que le programme fonctionne.

##  Problème

###  Phase 1. Choix du sujet
Chaque binôme choisit un sujet dans la liste ci-dessous.  

  - écrire un programme permettant de calculer toutes les racines carrées des nombres compris entre A et B, A et B étant
deux nombres entiers tels que A < B.
  - écrire un programme permettant d’afficher une matrice de taille MxN remplie par des nombres aléatoires compris entre
A et B. Les valeurs M, N, A et B doivent être passées en paramètres.

###  Phase 2. Pour le sujet choisi...
  - écrivez le squelette de la classe principale, et commentez-le.
  - écrivez l’intégralité de la classe test. Cette classe doit comprendre :
  - Des assertions comme vu précédemment.
  - Des tests vérifiant que les exceptions sont bien levées quand elles doivent l’être (par exemple : de mauvais paramètres
sont passés dans l’appel).
  - Des tests vérifiant que les boucles s’effectuent dans des temps raisonnables.
  - Formatez correctement les sorties de vos tests en utilisant les annotations @Before et @After.


<!-- ###  Phase 3. échange des sujets
  – échangez vos classes avec un binôme ayant traité un sujet différent du vôtre.
  – Implémentez la classe principale.
  – Appliquez les tests.
  – Itérez jusqu’à obtention d’un programme fonctionnel et satisfaisant l’ensemble des tests. -->
