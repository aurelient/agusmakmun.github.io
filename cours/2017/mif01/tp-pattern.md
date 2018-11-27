---
layout: page
title: Mif01 - TP Réingénierie et design patterns en JAVA
permalink: /cours/2017/mif01/tp-pattern.html
---

## Objectif
  Il vous est demandé d'effectuer une ré-ingénierie d'un
  code existant en mettant en oeuvre les patrons de conception vus en cours.


**Votre travail devra être rendu sous forme d'un projet déposé
    sur la Forge Lyon 1, au plus tard le dimanche 1 octobre à 23h59.**

Penser à remplir dès à présent le [questionnaire de rendu](https://goo.gl/forms/l6618dqPz6yaMwdx2) indiquant votre binome et votre dépôt forge. Le dépot ne sera relevé qu'après la date de rendu.


## Déroulement

Le travail peut être organisé en deux étapes :

  - la première sera une étape de ré-ingénierie (refactoring) du code utilisé dans les premiers TP, afin de mieux structurer le projet et le rendre plus modulaire.
  - la seconde sera dédiée à l'extension du projet pour réaliser un jeu plus complet.

### Partie 1 : Ré-ingénierie du code

Le code fourni lors de la première séance est un package relativement fouillis. Toutes les classes sont dépendantes les unes des autres, les couches graphique et métier ne sont pas séparées.

Il va vous falloir reconcevoir le code en appliquant les patrons de conception adéquats. Pour cela, vous devez réorganiser les éléments de l'application. Entre autres, l'affichage des joueurs doit être séparé de leur gestion (déplacements, stratégies, etc.).
Les changements dans le modèle métier (déplacements) devront être répercutés dans l'affichage.

L'utilisation d'entrées claviers ou souris entra&icirc;nera des changements dans le modèle métier en passant par un contrôleur.


### Partie 2 : Extension
On commencera par ajouter des éléments de contrôle au jeu pour le faire
démarrer, le mettre en pause, etc. On utilisera pour cela des widgets
javafx tels que des boutons.


Ajouter ensuite un mécanisme de contrôle des collisions en réfléchissant à son placement dans une architecture MVC. Les collisions peuvent être entre :

 - une balle et un joueur – **ce cas doit être géré obligatoirement**
 - une balle et les murs
 - une balle et un obstacle


Chaque joueur avec une IA aura une tactique propre qui consiste à :

 - se déplacer aléatoirement
 - suivre le joueur contrôlé par un humain

Toute autre stratégie est possible.

 - Faites en sorte que la tactique puisse être changée en cours de partie
  (via une action utilisateur sur un bouton par exemple).


Pour suivre et contrôler le jeu, on disposera de plusieurs vues:

 - une présentant le terrain
 - une autre présentant le score
 - une autre les contrôles du jeu


Au TP suivant nous rajouterons des *tests* permettant de vérifier qu'une balle ou un joueur ne sort jamais du terrain, et que les obstacles sont bien considérés.


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



## Rendu du TP / projet

### Projet Forge et questionnaire

Les projets peuvent être rendus en binômes. Les autres cours vont arriver
très vite, il est conseillé d'avoir presque terminé le week-end suivant le TP.

**Votre travail devra être rendu sous forme d'un projet déposé
    sur la Forge Lyon 1, au plus tard le dimanche 1 octobre à 23h59.**

Pensez à remplir dès à présent le [questionnaire de rendu](https://goo.gl/forms/l6618dqPz6yaMwdx2) indiquant votre binome et votre dépôt forge. Le dépot ne sera relevé qu'après la date de rendu.
**Ajoutez Aurélien TABARD et Lionel MEDINI en tant que "reporters".**


Votre dépôt sur la Forge devra contenir :

 - un fichier **README.txt** (ou .md) à la racine du projet
 - un fichier maven pour le build du projet
 - les sources (fichiers Java)
 - la documentation javadoc de vos classes
 - les fichiers natifs de votre modélisation UML (indiquez quel outil a été utilisé)
 - le rapport en PDF (6 pages maximum, format libre).

 Le rapport doit comprendre une présentation globale du projet,
 une motivation des choix d'architecture (et des patterns choisis),
 et leur explication en s'aidant de diagrammes appropriés et adaptés
 au degré de précision et au type d'explication.
 Donc des diagramme de classe, mais pas que cela, et pas de plats de spaghettis
 généré automatiquement représentant tout le code.


Barême indicatif (sur 27, remis sur 20) :

- Réalisation et exécution : 18 points
	- Clone git qui fonctionne (les bonnes personnes sont rapporteurs, la bonne branche est indiquée dans Spiral) (0,5 pts)
	- Compilation Maven (1 pts)
	- Code qui tourne directement sur l'ordinateur de l'évaluateur (1 pts)
	- Qualité du code (2 pts)
	- Structure globale du code, utilisation de Packages (0,5 pts)
	- README et respect des consignes	(1 pts)
	- Interface (UI) propre	(1 pts)
	- Stratégies __simples__ implémentées	(2 pts)
	- Gestion des tirs / touchés	(1 pts)
	- Tests	(3 pts)
	- Patterns mis en oeuvre (3 pts)

- Rapport et modélisation : 9 points
	- Qualité de la réalisation	Patterns utilisés (MVC est obligatoire + 3 autres minimums)	(3pts)
	- Modélisation des parties clés de l'application (3pts)
	- Explications	(3pts)
	- Les points suivants entrainent des malus (jusqu’à -5 pts)
	  - Contenu et forme (voir ci-dessus)
	  - Orthographe
