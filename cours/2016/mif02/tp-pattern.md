---
layout: page
title: Mif02 - TP Réingénierie et design patterns en JAVA
permalink: /cours/2016/mif02/tp-pattern.html
---

## Objectif
  Il vous est demandé d'effectuer une ré-ingénierie d'un
  code existant en mettant en oeuvre les patrons de conception vus en cours.
  Vous allez également concevoir une nouvelle application en utilisant
  le formalisme UML et en exploitant au maximum les procédures de
  génération de code et de rétro-conception.


  <strong>Votre travail devra être rendu sous forme d'un projet déposé
    sur la Forge Lyon 1, au plus tard le dimanche 2 octobre à 23h59.
  </strong>

  Penser à remplir dès à présent le [questionnaire Spiral](http://spiralconnect.univ-lyon1.fr/webapp/assessment/assessmentAnswer.html?id=6031795&mode=answer) indiquant votre binome et votre dépôt forge.


## Déroulement

Le travail peut être organisée en deux étapes :

  - la première sera une étape de ré-ingénierie (refactoring) du code de Poneymon utilisé au TP1, afin de mieux structurer le projet et le rendre plus modulaire.
  - la seconde sera dédiée à l'extension du projet pour réaliser un jeu plus complet.

### Partie 1 : Ré-ingénierie du code

Le code qui est fourni lors de la première séance est un package relativement fouillis. Toutes les classes sont dépendantes
les unes des autres, les couches graphique et métier ne sont pas séparées.

Il va vous falloir reconcevoir le code en appliquant les patrons de conception adéquats. Pour cela, vous devez réorganiser les éléments de
l'application Poneymon. Entre autres, l'affichage des poneys doit être séparé de leur gestion (déplacements, stratégies, etc.).
Les changements dans le modèle métier (déplacements) devront être répercutés dans l'affichage.

L'utilisation d'entrées claviers ou souris entra&icirc;nera des changements dans le modèle métier en passant par un contrôleur.


### Partie 2 : Extension
On commencera par ajouter des éléments de contrôle au jeu pour le faire
démarrer, le mettre en pause, etc. On utilisera pour cela des widgets
javafx tels que des boutons.


Ensuite rajouter des obstacles qui seront soit statiques, soit qui se
déplaceront en sens inverse des poneys. En cas de collision,
les poneys perdent de la vitesse.

 - Ajouter un mécanisme de contrôle des collisions en réfléchissant à son placement dans une architecture MVC.
 - Rajouter ensuite la gestion d'une action utilisateur permettant de sauter par dessus un obstacle.

Chaque poney avec une IA aura une tactique propre [(voir fin du TP remise en route Java)](/cours/2016/mif02/tp-java.html).

 - Adapter les stratégies pour que l'IA puisse éviter les collisions.
 - Faites en sorte que la tactique puisse être changée en cours de partie
  (via une action utilisateur sur un bouton par exemple).


Pour suivre et contrôler la course, on disposera de plusieurs vues:

 - une présentant du terrain de course
 - une autre présentant le score
 - une autre les contrôles du jeu


Rajouter des *tests* permettant de vérifier qu'un Poney ne part jamais en arrière, et un obstacle en avant.

### Conseils pour la réalisation

Faites un modèle du domaine du jeu que vous voulez mettre en place :
  acteurs, caractéristiques des acteurs, obstacles, tactique, etc.
  Organisez vos classes en packages pertinents.

Pensez à utiliser les patterns de création, mais aussi de structure et de comportement.

<!-- <p>Une fois vos classes de conception à peu près stabilisées, générez le code correspondant
à votre projet, et utilisez éventuellement la procédure de
<i>round trip engineering</i> pour synchroniser en permanence code et modèle. Parmi les applications de modélisation UML, vous pouvez utiliser
<a href="http://argouml.tigris.org/">ArgoUML</a>, <a href="http://www.bouml.fr/">BoUML</a>, <a href="http://www.altova.com/umodel.html">UModel</a>... Vous pouvez également utiliser des plugins UML pour <a href="http://plugins.netbeans.org/PluginPortal/">Netbeans</a> ou <a href="http://www.eclipse.org/modeling/mdt/?project=uml2">Eclipse</a>.
 -->



<!--
<h3>Introduction : outils UML</h3>
<p>UModel est  un des outils disponibles à l'UFR informatique pour la modélisation et le roundtrip engineering.
Mettez rapidement en place un cycle de roundtrip engineering, par exemple sur les Tortues du package <a href="doc/MIF17/logo.tar.gz">logo</a> de base.
<p>Remarque : Netbeans 2.9 n'a plus de composant UML, Netbeans 2.7 en a toujours un qui fonctionne bien.  Si vous êtes sur votre machine personnelle,
vous  pouvez utiliser n'importe quel outil UML pour tester les fonctionnalités de roundtrip engineering.<br>

<p>Au cours du projet, en phase codage, vous pourrez utiliser l'outil UML de votre choix en mettant en place un cycle de roundtrip engineering.
-->



## Rendu du TP

### Projet Forge et questionnaire

Les projets peuvent être rendus en binômes. Les autres cours vont arriver
très vite, il est conseillé d'avoir presque terminé le week-end suivant le TP.

Votre dépôt sur la Forge devra contenir :

 - un fichier README.txt à la racine du projet
 - un fichier maven pour le build du projet
 - les sources (fichiers Java)
 - la documentation javadoc de vos classes
 - les fichiers natifs de votre modélisation UML (indiquez quel outil a été utilisé)
 - le rapport en PDF (6 pages maximum, format libre).

 Le rapport doit comprendre une présentation globale du projet,
 une motivation des choix d'architecture (et des patterns choisis),
 et leur explication en s'aidant de diagrammes appropriés et adaptés
 au degré de précision et au type d'explication.
 Donc des diagramme de classe, mais pas que cela, et pas de plat de spaghettis
 illisible représentant tout le code et généré automatiquement


Barême indicatif :

- Réalisation : 7 points
  - Respect des consignes (voir ci-dessus)
  - Implémentation de l'interface
  - Implémentation de stratégies _simples_
  - Gestion des collisions
  - Mise en ouvre des tests
  - Mise en oeuvre des patterns
  - Fonctionnement et qualité de l'exécution
- Rapport : 5 points
  - Contenu et forme (voir ci-dessus)
  - Orthographe
  - Explication des patterns (liens diagrammes - explications)
- Modélisation : 3 points
  - Patrons utilisés
  - Diagrammes fournis

Dans la configuration de votre projet, ajoutez Aurélien TABARD et
Lionel MEDINI en tant que "reporters".
Remplissez également le questionnaire Spiral, ce qui permettra aux
intervenants de récupérer automatiquement les projets :
[Questionnaire Spiral](http://spiralconnect.univ-lyon1.fr/webapp/assessment/assessmentAnswer.html?id=6031795&mode=answer)
