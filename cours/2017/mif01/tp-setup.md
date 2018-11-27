---
layout: page
title: Mif01 - TP Maven-Git-Forge
permalink: /cours/2017/mif01/tp-setup.html
---

[Revenir a la page du cours](.)

## Objectif

Mettre en place et maitriser les outils de gestion de code utilisés tout au long de l'année.

 - Outil de build avec Maven (mvn)
 - Outil de versioning avec Git (git)
 - Outil de gestion de projet avec Gitlab (la Forge)



## Déroulement
Ce TP est à réaliser de préférence sous Linux (accès à mvn et git en ligne de commande).
L'utilisation d'IDE est n'est pas recommandée pour ce TP.


### Démarrage

**Créer un nouveau projet sur la forge** : [forge.univ-lyon1.fr](http://forge.univ-lyon1.fr) → **+** → Nouveau Projet.

Si vous vous connectez pour la première fois, le système vous permettra de vérifier/modifier les informations qui vous concernent, idem pour votre éventuel binôme. Ajouter ce dernier comme développeur de votre projet (Configuration → Membres).

Sur votre ordinateur, dans un terminal, ajoutez les informations de base à votre compte git :

~~~~~~~
git config --global user.name "Nom Prenom"
git config --global user.email "votre_email@etu.univ-lyon1.fr"
~~~~~~~

Toujours dans un terminal, déplacez vous dans le dossier ou vous souhaitez créer le projet, et clonez votre dépôt git. L'URL de votre dépôt est accessible dans Gitlab depuis la page du projet :

~~~~~~~~
git clone git@forge.univ-lyon1.fr:NomdUtilisateur/NomDeVotreRepo.git
~~~~~~~~

[En cas de problème, voir la faq de la forge](https://forge.univ-lyon1.fr/EMMANUEL.COQUERY/forge/wikis/FAQ), et le guide de Titouan Chary (M2) pour [accéder à la forge depuis l'extérieur](https://forge.univ-lyon1.fr/tchary/transparent_forge).

Se placer dans le répertoire du et récupérer des modifications depuis le projet balleauprisonnier_2017:

~~~~~~~~
git pull http://forge.univ-lyon1.fr/aurelien.tabard/balleauprisonnier_2017.git
~~~~~~~~
<!--
puis mettre à jour à la dernière version

~~~~~~~~
git update
~~~~~~~~ -->

Ce projet est constitué d'un projet maven (nommé balleauprisonnier_mvn dans le fichier pom.xml).

Reverser dans votre projet forge:

~~~~~~~~
git push -u origin master
~~~~~~~~

Dans le navigateur, naviguer dans le dépôt: vous pouvez voir les révisions déjà présentes et même regarder le code source en ligne, ainsi que les différences entre les révisions.

### .gitignore et gestion d'un ticket

Depuis le projet forge, créer une nouvelle demande (*issue*) intitulée: “ignorer le répertoire target”. Ce dossier target sera créé par maven au moment du build, et contiendra les fichier .class et le jar.

Accéder à la liste des demandes de votre projet, puis à la demande précédente. Modifier cette demande en assignant un des membres du projet à cette tâche. Poursuivre le TP puis revenir à la demande et la marquer comme fermée (*closed*) une fois le travail terminé. Noter le numéro #xxxx de la demande.

<!-- Dans le répertoire de travail, lancer

~~~~~~~~
hg status
~~~~~~~~

Il y a de nombreux fichiers non gérés sous le répertoire target. -->

Créer un fichier .gitignore à la base du répertoire de travail balleauprisonnier et y ajouter les lignes suivantes :

~~~~~~~~
# Ignore les fichiers de configuration d'Eclipse
.classpath
.project
.settings/

# Ignore les fichiers de configuration d'Intellij
.idea/
*.iml
*.iws

# Ignore le dossier Mac .DS_Store
.DS_Store

# Ignore les fichiers produits par Maven pour ne versionner que le code,
# pas les executables ou les logs.
log/
target/
~~~~~~~~

ce fichier contient la liste des fichiers à ignorer par git.

~~~~~~~~
git status
~~~~~~~~

n'affiche à présent plus les fichiers dans target, mais affiche le fichier .gitignore. Ajouter ce fichier dans les fichiers versionnés:

~~~~~~~~
git add .gitignore
~~~~~~~~

puis valider en indiquant le numéro de la demande #xxxx dans le message de commit:

~~~~~~~~
git commit -m "Gestion des fichier à ignorer (bug #xxxx)"
~~~~~~~~

puis faire le push

~~~~~~~~
git push
~~~~~~~~

Dans le projet forge, aller voir le dépôt et cliquer sur le dernier commit et ajouter une demande liée en spécifiant votre numéro de ticket. Cliquer ensuite sur le lien vers la demande depuis le message de commit.

<!-- Passer le statut de la demande à “closed” en indiquant le numéro de la révision précédé de la lettre r5) ou le hash du commit précédé de commit: dans les notes de mise à jour). -->

### Invocation de maven

Regarder le code de la classe balleauprisonnier_mvn.App du module balleauprisonnier_mvn (fr/univ_lyon1/info/m1/balleauprisonnier_mvn/App.java).

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

En pratique on veut souvent nettoyer le dossier target, et relancer le processus de build, tests compris :

~~~~~~~~
mvn clean install
~~~~~~~~

Pour lancer l'application en ligne de commande on utilise :

~~~~~~~~
java -cp target/balleauprisonnier_mvn-0.0.1.jar fr.univ_lyon1.info.m1.balleauprisonnier_mvn.App
~~~~~~~~

S'il n'y a pas d'erreur, enregistrer les modifications, puis poussez les vers votre dépôt:

~~~~~~~~
git commit -m "un message explicatif ici"
git push -u origin master
~~~~~~~~

Constater que les modifications sont visibles depuis site de votre projet forge.

<!-- > Si git se plaint que vous n'avez pas spécifié de nom d'utlisateur, deux choix:
>
>    Utiliser l'argument -u "mon nom <mon.email@mon.domaine>"  
>    Modifier votre configuration mercurial en ajoutant au fichier ~/.hgrc (doc)

> ~~~~~~~~
>    [ui]
>    username = John Doe <john@example.com>
> ~~~~~~~~ -->


### Packaging

Configurer le plugin `maven-assembly-plugin` pour générer un jar exécutable incluant les bibliothèques utilisées (voir [ici](http://stackoverflow.com/questions/574594/how-can-i-create-an-executable-jar-with-dependencies-using-maven)).

Tester en lancer java via

~~~~~~~~
java -jar target/balleauprisonnier_mvn-0.0.1-jar-with-dependencies.jar
~~~~~~~~


### Gérer les conflits

Nous n'allons pas mettre en pratique la gestion de conflits dans ce TP, mais c'est quelque chose qui arrive fréquement.
La [documentation de Git traite du sujet](https://git-scm.com/book/fr/v2/Les-branches-avec-Git-Branches-et-fusions%C2%A0%3A-les-bases)), et [Github a un guide expliquant plutôt bien les choses](https://help.github.com/articles/resolving-a-merge-conflict-using-the-command-line/).

Pour lancer la fusion des deux branches avec on utilise la commande merge:

~~~~~~~~
git merge
~~~~~~~~

Le conflits interviennent souvent lors du pull d'une branche dans la branche courante.
Cette commande importe les modification de la branche crée lors du pull dans la branche courante.

git status signale les fichiers en conflits. Editer ces fichiers pour intégrer de manière cohérente les modifications effectuées dans le deux branches. Une fois les modifications effectuées, si la construction mvn install fonctionne, indiquer ques les conflits sont résolus via

~~~~~~~~
git resolve -m le_fichier_concerne
~~~~~~~~
