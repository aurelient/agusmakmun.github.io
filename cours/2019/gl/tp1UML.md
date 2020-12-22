---
layout: page
title: TP 1 UML - Diagrammes Statiques
permalink: /cours/2019/gl/tp1UML.html
---



## TP Diagramme de classe

Vous travaillez sur un projet de gestion de véhicules autonomes qui se déplacent "à la main" et en flotte autonome sur l’autoroute. Modéliser l'application suivante.

Véhicule et flotte :

1. Une flotte est composée de 2 à 20 véhicules
2. Une flotte possède toujours un meneur suivi du reste des véhicules.
3. Un véhicule est caractérisé par un identifiant, sa vitesse maximum, son volume et une position dans la flotte.
4. Un véhicule peut être une voiture, une camionnette ou un camion.
5. Le meneur est un véhicule en charge de calculer la vitesse et l’itinéraire optimal pour la flotte en terme de temps et de consommation énergétique.
6. Les voitures sont caractérisées par leur nombre de passagers, les camions et camionnettes par leur charge.

Trajet :

1. Chaque véhicule a un trajet propre.
2. Chaque trajet est caractérisé par un échangeur d’autoroute de début et de fin, par date et une heure de départ et d’arrivée, et composé de tronçons correspondant à deux échangeurs qui se suivent.
3. Un échangeur est définit par un nom et un numéro.
4. Le véhicule connait son trajet courant, mais conserve aussi un historique de tous ses trajets passé.
5. Chaque tronçon est défini par une heure de début et de fin, ainsi que par une distance.

Décrire au travers d’un diagramme de classe comment sont organisées les classes d'une application permettant d'implémenter ce système.

Commencer par vous demander quels sont les classes en présence.

Puis modéliser leurs relations les unes aux autres.

Penser à abstraire/généraliser les classes qui ont des parties communes au besoin.


On utilisera [draw.io](draw.io)


## Rendu

Les TPs compterons pour 50% de la note.

Le TP peut se faire seul ou en binôme.

Le rendu se fait en deux fois :  

1. v1 en fin de TP  _il est possible d'avoir terminé à ce moment là_ [Formulaire Tomuss :  TP1_rendu_seance_(pdf)](https://tomuss.univ-lyon1.fr/2019/Automne/UE-INF2108M).
2. v2 avant dimanche 1 décembre 23h59 [Formulaire Tomuss :  TP1_rendu_final_(pdf)](https://tomuss.univ-lyon1.fr/2019/Automne/UE-INF2108M).

**L'évaluation se fera à 75% sur la v1**, la v2 permettra de finaliser/nettoyer le TP.

L'architecture peut prendre des formes assez diverses, des rendus trop similaire entre groupes seront sanctionnés.
