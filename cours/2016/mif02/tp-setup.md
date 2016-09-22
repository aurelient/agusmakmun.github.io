---
layout: page
title: Mif02 - TP Maven-Mercurial-Forge
permalink: /cours/2016/mif02/tp-setup.html
---

[Revenir a la page du cours](.)

## Objectif

Mettre en place et maitriser les outils de gestion de code utilisés tout au long de l'année.

 - Outil de build avec Maven (mvn)
 - Outil de versioning avec Mercurial (hg)
 - Outil de gestion de projet avec Redmine (la Forge)

Ceci est une version révisée pour le Mif02 du [TP générique d'Emmanuel Coquery](http://liris.cnrs.fr/ecoquery/dokuwiki/doku.php?id=enseignement:tp:forge-maven).

## Déroulement
Ce TP est à réaliser de préférence sous Linux (accès à mvn et hg en ligne de commande).
L'utilisation d'IDEs est n'est pas recommandée pour ce TP.


### Démarrage

Créer un nouveau projet sur la forge (http://forge.univ-lyon1.fr → Projets → Nouveau Projet). Si vous vous connectez pour la première fois, le système vous permettra de vérifier/modifier les informations qui vous concernent, idem pour votre éventuel binôme. Ajouter ce dernier comme développeur de votre projet (Configuration → Membres)

Clonez votre dépôt mercurial dans un répertoire poneymon1. L'URL de votre dépôt est accessible dans Redmine depuis votre projet via Configuration → Dépôt:

~~~~~~~~
hg clone https://forge.univ-lyon1.fr/hg/NomDeVotreRepo      poneymon1
~~~~~~~~

> En cas de warning de sécurité [voir la faq de la forge](http://forge.univ-lyon1.fr/projects/forge/wiki/FAQ)

Se placer dans le répertoire poneymon1 et récupérer des modifications depuis le projet poneymon_v0:

~~~~~~~~
hg pull https://forge.univ-lyon1.fr/hg/poneymon_v0
~~~~~~~~

puis mettre à jour à la dernière version

~~~~~~~~
hg update
~~~~~~~~

Ce projet est constitué d'un projet maven (nommé poneymon_mvn dans le fichier pom.xml).

Reverser cette mise à jour dans votre projet forge:

~~~~~~~~
hg push
~~~~~~~~

Dans le navigateur, naviguer dans le dépôt: vous pouvez voir les révisions déjà présentes et même regarder le code source en ligne, ainsi que les différences entre les révisions.

## .hgignore et gestion d'un ticket

Depuis le projet forge, créer une nouvelle demande intitulée: “ignorer le répertoire target”. Ce dossier target sera créé par maven au moment du build, et contiendra les fichier .class et le jar.

Accéder à la liste des demandes de votre projet, puis à la demande précédente. Modifier cette demande en assignant un des membres du projet à cette tâche, passez son status à “In progress” et valider. Noter le numéro #xxxx de la demande.

<!-- Dans le répertoire de travail, lancer

~~~~~~~~
hg status
~~~~~~~~

Il y a de nombreux fichiers non gérés sous le répertoire target. -->

Créer un fichier .hgignore à la base du répertoire de travail poneymon1 et y ajouter les lignes suivantes :

~~~~~~~~
    syntax: glob
    target
~~~~~~~~

ce fichier contient la liste des fichiers à ignorer par mercurial.

~~~~~~~~
hg status
~~~~~~~~

n'affiche à présent plus les fichiers dans target, mais affiche le fichier .hgignore. Ajouter ce fichier dans les fichiers versionnés:

~~~~~~~~
hg add .hgignore
~~~~~~~~

puis valider en indiquant le numéro de la demande #xxxx dans le message de commit:

~~~~~~~~
hg commit -m "Gestion des fichier à ignorer (bug #xxxx)"
~~~~~~~~

puis faire le push

~~~~~~~~
 hg push
~~~~~~~~

Dans le projet forge, allez voir le dépôt et cliquez sur le dernier commit et ajouter une demande liée en spécifiant votre numéro de ticket. Cliquer ensuite sur le lien vers la demande depuis le message de commit.

Passer le statut de la demande à “closed” en indiquant le numéro de la révision précédé de la lettre r5) ou le hash du commit précédé de commit: dans les notes de mise à jour6).

### Invocation de maven

Regarder le code de la classe poneymon_mvn.App du module poneymon_mvn (fr/univ_lyon1/info/m1/poneymon_mvn/App.java).

Invoquer

~~~~~~~~
mvn compile
~~~~~~~~

à la racine du projet et constater que la construction du projet est bien déclenchée.

Le répertoire target contient tout ce qui est généré par maven. Explorer le contenu du répertoire, puis invoquer

~~~~~~~~
mvn clean
~~~~~~~~

Regarder ce qui a été supprimé.


<!-- ### Correction de code

Exécuter les tests unitaires:

~~~~~~~~
mvn test
~~~~~~~~

La construction échoue. Pour comprendre quelle est le problème, regarder le fichier bonjour/target/surefire-reports/bonjour.AppTest.txt

Corriger la classe bonjour.App pour générer le bon message et passer le test unitaire. -->

On lancer les tests associés au projet avec:

~~~~~~~~
mvn test
~~~~~~~~

La phase de vérification doit fonctionner car aucun test unitaire n'est réellement implémenté pour le moment, nous verrons cela dans un TP suivant.

En pratique on appelle souvent, ce qui permet de nettoyer le dossier target, et de relancer le processus de build, tests compris :

~~~~~~~~
mvn clean install
~~~~~~~~

Pour lancer l'application en ligne de commande on utilise :

~~~~~~~~
java -cp target/poneymon_mvn-0.0.1.jar fr.univ_lyon1.info.m1.poneymon_mvn.App
~~~~~~~~

S'il n'y a pas d'erreur, enregistrer les modifications, puis poussez les vers votre dépôt:

~~~~~~~~
hg commit -m "un message explicatif ici"
hg push
~~~~~~~~

Constater que les modifications sont visibles depuis site de votre projet forge.

> Si mercurial se plain que vous n'avez pas spécifié de nom d'utlisateur, deux choix:
>
>    Utiliser l'argument -u "mon nom <mon.email@mon.domaine>"  
>    Modifier votre configuration mercurial en ajoutant au fichier ~/.hgrc (doc)

> ~~~~~~~~
>    [ui]
>    username = John Doe <john@example.com>
> ~~~~~~~~


### Packaging

Configurer le plugin `maven-assembly-plugin` pour générer un jar exécutable incluant les bibliothèques utilisées (voir [ici](http://stackoverflow.com/questions/574594/how-can-i-create-an-executable-jar-with-dependencies-using-maven)).

Tester en lancer java via

~~~~~~~~
java -jar target/poneymon_mvn-0.0.1-jar-with-dependencies.jar
~~~~~~~~


### Gérer les conflits

Nous n'allons pas mettre en pratique la gestion de conflits dans ce TP, mais c'est quelque chose qui arrive fréquement.
La [documentation de Mercurial traite du sujet](http://mercurial.selenic.com/wiki/TutorialConflict)).

Pour lancer la fusion des deux branches avec on utilise la commande merge:

~~~~~~~~
hg merge
~~~~~~~~

Le conflits interviennent souvent lors du pull d'une branche dans la branche courante.
Cette commande importe les modification de la branche crée lors du pull dans la branche courante.

hg status signale les fichiers en conflits avec la lettre M. Editer ces fichiers pour intégrer de manière cohérente les modifications effectuées dans le deux branches. Une fois les modifications effectuées, si la construction mvn install fonctionne, indiquer ques les conflits sont résolus via

~~~~~~~~
hg resolve -m le_fichier_concerne
~~~~~~~~



<!-- #### Work2: commons-cli

Cloner à nouveau votre projet dans un deuxième répertoire de travail work2.

~~~~~~~~
hg clone https://.....   work2
~~~~~~~~

Ajouter la dépendance vers apache-commons-cli au bon endroit dans le pom.xml du projet bonjour:

~~~~~~~~
<dependency>
   <groupId>commons-cli</groupId>
   <artifactId>commons-cli</artifactId>
   <version>1.2</version>
</dependency>
~~~~~~~~

Consulter la documentation et utiliser la bibliothèque commons-cli pour ajouter un argument en ligne de commande correspondant au nom de la personne à saluer. Le traitement des options se fera dans une méthode `public void init(String [] args)` de la classe Bonjour. Dans le main l'appel `app.setPersonne(“Toto”)` sera remplacé par un appel à `app.init(args)`.

Utiliser un `new BasicParser();`

Le package de commons-cli est `org.apache.commons.cli`

L'exécution via le jar comme précédement ne fonctionne plus. A la place on peut utiliser la commande suivante depuis le projet bonjour:

~~~~~~~~
mvn exec:java -Dexec.mainClass=bonjour.App
~~~~~~~~

L'affichage se fait bien ... mais est perdu dans les logs.

Pour passer les arguments en ligne de commande, ajouter `-Dexec.args=“-foo bar”,` exemple:

~~~~~~~~
mvn exec:java -Dexec.mainClass=bonjour.App -Dexec.args="-u Titi"
~~~~~~~~

Valider les modifications:

~~~~~~~~
hg commit -m 'ajout de commons-cli'
~~~~~~~~

Ne pas faire de push à ce niveau

#### Work1: slf4j

Dans le répertoire work1 (qui ne contient pas les modifications précédentes) ajouter au projet bonjour les dépendances vers slf4j et logback:

   slf4j-api pour la compilation (et l'exécution)

~~~~~~~~
<dependency>
   <groupId>org.slf4j</groupId>
   <artifactId>slf4j-api</artifactId>
   <version>1.7.5</version>
</dependency>
~~~~~~~~

Chercher logback-classic sur http://search.maven.org/ , sélectionner la version 1.0.13 et ajouter les informations de dépendances (visibles à gauche de la page). Ajouter `<scope>runtime</scope>` pour limiter l'inclusion de cette dépendance à l'exécution.

L'utilisation de slf4j dans ses versions récentes nécessite une version de java >= 1.5

Ajouter à l'élément project du pom du projet bonjour le code suivant pour configurer le plugin de compilation:

~~~~~~~~
 <build>
   <plugins>
     <plugin>
       <groupId>org.apache.maven.plugins</groupId>
       <artifactId>maven-compiler-plugin</artifactId>
       <version>3.1</version>
       <configuration>
         <source>1.8</source>
         <target>1.8</target>
       </configuration>
     </plugin>
   </plugins>
 </build>
~~~~~~~~

Modifier la classe bonjour.App pour faire l'affichage via un logger slf4j (c.f. documentation).

Valider les modifications

~~~~~~~~
hg commit -m 'affichage via slf4j'
~~~~~~~~

Utiliser `mvn exec:java` pour lancer votre application

L'affichage diffère d'un `System.out.println()`

#### Work1: fusion des modifications

Toujours depuis le répertoire work1, faire un pull des modifications du dépôt local work2:

~~~~~~~~
hg pull ../work2
~~~~~~~~

Mercurial se plain de l'apparition d'une nouvelle tête anonyme correspondant à une nouvelle branche.

Lancer la fusion des deux branches avec

~~~~~~~~
hg merge
~~~~~~~~

Cette commande importe les modification de la branche crée lors du pull dans la branche courante.

Cette modification créée des conflits sur la classe bonjour.App et sur le fichier pom.xml du projet bonjour. hg status les signale comme étant modifiés avec la lettre M. Editer ces fichiers pour intégrer de manière cohérente les modifications effectuées dans le deux branches. Une fois les modifications effectuées, si la construction mvn install fonctionne, indiquer ques les conflits sont résolus via

~~~~~~~~
hg resolve -m le_fichier_concerne
~~~~~~~~

(voir la [doc](http://mercurial.selenic.com/wiki/TutorialConflict)).

Valider et transmettre les modifications:
 - Valider avec commit.
 - Faire un push sur le dépôt de la forge.
 - Dans work2, faire un pull depuis la forge
 - Dans work2, faire un pull depuis work1 et constater qu'aucune modification supplémentaire n'est transmise.
 - Dans work2, faire hg update pour avoir une copie de travail à jour de la dernière version. -->
