# O.D.E.V.A.

**O**utils supportant le **DEV**eloppement, le déploiement et la maintenance collaborative des **A**pplications



# Collaborer

[https://github.com/seblucas/odeva](https://github.com/seblucas/odeva)



# Projet

L'art de travailler ensemble.


# Cycle de vie

 * Analyse
 * Développement
 * Livraison / Recette
 * Mise en production
 * Maintenance


# Pas si simple

 * Livraison par bloc
 * Travail en équipe (offshore)
 * Maintenance (plusieurs années)
 * Plusieurs clients
 * Stress
 * Qualité


# La réalité

> "Un chef de projet est la seule personne au monde à croire que 9 femmes peuvent faire 1 bébé en 1 mois"
> 
> "7 projets informatiques sur 10 ne réussissent pas dans les temps ou pire encore jamais" Codendi


# Besoin de certitude

Une projet se reussit en agissant sur les faits et en travaillant en vérité avec le client, sa hiérarchie et ses collaborateurs.

[C'est presque fini](http://geekandpoke.typepad.com/geekandpoke/2012/10/doad.html)



# Besoin d'outils

![SCM Central](images/ScmCentral.png)



# Autres outils


# Wiki

 * Seule source 100% fiable
 * Ouvert à l'extérieur
 * Construit au fur et à mesure
 * Aide mémoire.


# Intégration continue
 * Jenkins, Teamcity, Bamboo, Travis, ...
 * Compilation automatique
 * Test unitaires
 * Test d'intégration
 * Génération artefacts


# Déploiement auto
 * Cela devient une réalité
 * Déploiement simplifié.
 * Github, Facebook, Google



# SCM


# Lexique

 * SCM (**S**ource **C**ode **M**anagement)
 * VCS (**V**ersion **C**ontrol **S**ystem)
 * SCV (**S**ystême de **C**ontrôle de **V**ersion)


# Historique

 * SCCS: 1972, Bell Labs, Marc J. Rochkind
 * diff: 1974, AT&T, Hunt-McIlroy algorithm
 * RCS: 1982, GNU, Walter F. Tichy
 * patch: 1985, Larry Wall
 * CVS: 1986, Dick Grune
 * Subversion: 2000, CollabNet, Apache
 * Git: 2005, Linus Torvalds


# 2016

Toutes les sociétés n’utilisent pas encore de SCM !


# Principe
 * Plusieurs développeurs travaillent ensemble sur le même projet
 * Chacun dispose de sa copie locale
 * Chacun met à disposition des autres les dernières modifications
 * Co-développement, contrôle de distributions, maintenance.
 * Évolution des changements subis par un ensemble de fichiers


![SCM Schéma](images/ScmGraphe.png)



# Tickets


# Principe

 * Liste de choses à faire !
 * Ne pas oublier les petites tâches.
 * Les relire constamment.
 * Aide mémoire.


# Comment bien les utiliser
 * Qui, Quand, Quoi, Pourquoi, Comment, Ou ?
 * Catégorie : Bug, Evolution, ...
 * Étiquettes (Tag).
 * Jalon (Milestone).
 * Propriétaire.
 * Ordonnancement.
 * Phrases à bannir !


# Worflow

![Trac Workflow](images/TracWorkflow.png)


# Historique
 * Historique d'un client.
 * Qu'est ce qui a été livré ?
 * Comment a-t-on clôturé un ticket ?
 * Statistiques.



# Petit projet ?


# Exemple petit projet individuel

 * Un service REST en PHP
 * Un contrôleur AngularJS en Javascript
 * Une vue HTML
 * Des dépendances externes (librairies AngularJS, framework CSS, framework PHP, ...)


# Architecture

```bash
user@home:~/src/projet1# ls
Modele.php
Controleur.js
Vue.html
vendor
```


# Nouveaux besoins

 * L'évolution d'un projet informatique n'est pas linéaire (beaucoup de retours en arrière).
 * Besoin de sauvegarde.
 * Envie de garder à disposition la dernière version fonctionnelle.


# Nouvelle architecture

```bash
user@home:~/src/projet1# ls
Modele.bak
Modele.php
Controleur.bak
Controleur.js
Vue.bak
Vue.html
vendor
```


# Nouveaux besoins

 * Besoin de sauvegardes plus anciennes
 * Besoin de trouver des ensembles cohérents


# Nouvelle architecture

```bash
user@home:~/src/projet1# ls
Modele.php.20140302
Modele.php.20140407
Modele.php
Controleur.js.20140302
Controleur.js
Vue.html.20140407
Vue.html
vendor
```

**Cela commence à être complexe**


# Nouveaux besoins

 * Sauvegarde historisée (mail, dropbox, ...).
 * Un fichier texte est ajouté sur chaque répertoire pour préciser ce qui est fait et ce qui reste à faire (aide mémoire).
 * Utilisation régulière de la commande `diff` pour se souvenir des différences de code.


# Deux semaines après : besoin de cohérence

```bash
user@home:~/src# ls
projet1_20140502
projet1_20140503
projet1_20140504
projet1
```


# Bilan sur un projet individuel

 * Besoin d'un historique.
 * Besoin de sauvegarde.
 * Besoin de cohérence.
 * Besoin d'un aide mémoire (texte, `diff`)



# Subversion


# Création

```bash
cd /home/user/svn
svnadmin create monProjet
mkdir /tmp/Projet
mkdir /tmp/Projet/branches
mkdir /tmp/Projet/tags
mkdir /tmp/Projet/trunk
svn import /tmp/Projet file:///home/user/svn/monProjet -m "Import initial"
```


# Copie locale

```bash
cd /home/user/src
svn co file:///home/user/svn/monProjet/trunk maCopieLocale
cd maCopieLocale
```


# svnserve / Apache (dav)

```bash
vi /home/user/svn/monProjet/conf/svnserve.conf
# anon-access = read -> anon-access = write
svnserve -d -r /home/user/svn --listen-port 45001 --foreground
```

```bash
svn co svn://ip:45001/monProjet/trunk distance
```


# Check in / Commit

![Add](http://betterexplained.com/wp-content/uploads/version_control/basic_checkin.png)

```bash
touch list.txt
svn add list.txt
(Modifier le fichier)
svn status
svn ci list.txt -m "Ajout de XXX dans la liste"
```


# Check out / Mise à jour

![Checkout](http://betterexplained.com/wp-content/uploads/version_control/checkout_edit.png)

```bash
svn co http://path/to/trunk
svn up
svn revert list.txt
```


# Historique / Différences

![Diff](http://betterexplained.com/wp-content/uploads/version_control/basic_diffs.png)

```bash
svn log list.txt
svn diff -r3:4 list.txt
```


# Etiquettes / Version

![Tag](http://betterexplained.com/wp-content/uploads/version_control/tagging.png)

```bash
svn copy http://path/to/revision http://path/to/tag
```


# Branches

![Branch](http://betterexplained.com/wp-content/uploads/version_control/first_branch.png)

```bash
svn copy http://path/to/trunk http://path/to/branch
```


# Fusion

![Merge](http://betterexplained.com/wp-content/uploads/version_control/merging.png)

```bash
svn merge -r5:6 http://path/to/branch
```


# Conflits

![Conflit](http://betterexplained.com/wp-content/uploads/version_control/vcs_conflict.png)

Gestion manuelle la plupart du temps.



# Git


# Centralisé

![Centralisé](http://betterexplained.com/wp-content/uploads/version_control/distributed/centralized_example.png)


# Décentralisé / Distribué

![Decentralisé](http://betterexplained.com/wp-content/uploads/version_control/distributed/distributed_example.png)


# Avantages DVCS

 * L'historique des versions est toujours disponible
 * Les commits sont toujours possibles (même offline)
 * Beaucoup plus rapide
 * Facilité de création de branches
 * Moins de maintenance


# Plus de complexité

 * La manière de collaborer n'est pas forcée par le système
 * Impossible de savoir où est la dernière version
 * Besoin de cadrer l'organisation.
 * Les numéros de version sont des GUID


# Push / Pull

![PushPull](http://betterexplained.com/wp-content/uploads/version_control/distributed/distributed_push_pull.png)


# Github / Pull request

 * Les contributeurs font des PR
 * Le mainteneur les accepte, les refuse ou demande des modifications
 * Notion de `rebase` pour réécrire l'histoire.
 * Git flow

Nouveau rôle : Intégrateur.



# Les commandes GIT

 [La meilleure source à mon avis](http://ndpsoftware.com/git-cheatsheet.html)

Proxy : [Trac ODEVA](http://forge.fil.univ-lille1.fr/eODEVA/wiki/ReglageProxySCV)



# Git / Basique


# TP / Commandes à connaitre

```bash
git log
git diff (--cached)
git status
```


# TP / Basique

```bash
cd /home/user/src
git init testGit
git clone testGit testGitLocal
cd testGitLocal/
touch a.txt && git add a.txt
git commit -am "Ajout de a.txt"
```


# TP / Branches

```bash
git checkout -b modif
git branch
touch b.txt && git add b.txt
git commit -am "Ajout de b.txt"
git checkout master
touch c.txt && git add c.txt
git commit -am "Ajout de C.txt"
git merge modif
```


# TP / Push

```bash
cd ../testGit
git config --bool core.bare true
cd ../testGitLocal
git remote -v
git push origin master
```


# TP / .gitignore

[gitignore.io](https://www.gitignore.io)

```bash
cd ../testGitLocal
nano .gitignore
git add .gitignore
git commit -am "Ajout de la liste des ignorés"
git push origin master
```


# TP / pull rebase

```bash
cd /home/user/src
git clone testGit testGitDeux
cd testGitDeux
touch z.txt && git add z.txt
git commit -am "Add z"
git push origin master
cd ../testGitLocal
touch y.txt && git add y.txt
git commit -am "Add y"
git pull --rebase origin master
git push origin master
```


# TP / Conflits

```bash
cd ../testGitDeux
echo "Modification A" >> a.txt
git commit -am "Modification a.txt"
git push origin master
cd ../testGitLocal
echo "Modification B" >> a.txt
git commit -am "Modification a.txt"
git pull --rebase
git push origin master
```


# Grands pouvoirs


# Intérêts

 * Avoir le droit de changer d’avis
 * Tester des idées sans conséquence
 * Collaborer avec d’autres personnes
 * Faciliter la **maintenance** ou le déboggage


# Intérêts (suite)
 * Générer des statistiques
 * Gagner du temps
 * Garder sa santé mentale


# Intérêts (suite)
 * Log
 * Blame / Annotate
 * Bisect


# Revue de code

Pas de revue de code sans gestionnaire de source.

Excellent moyen d'apprendre !


# Outils graphiques

[TortoiseSVN](http://tortoisesvn.net/), [TortoiseHG](http://tortoisehg.bitbucket.org/), [Github](https://github.com/), [Bitbucket](https://bitbucket.org/), [SourceTree](https://www.sourcetreeapp.com/), [Github Desktop](https://desktop.github.com/), ...



# Grandes responsabilités


# Rien de magique !

 * Un SCM mal utilisé sera certainement plus pénalisant que de ne pas en utiliser.
 * Ce n'est pas le SCM qui va permettre de gérer la communication autour du projet.
 * Un SCM se sauvegarde !
 * Ne jamais toucher aux fichiers internes (.svn, .git, ...)


# Fichiers à exclure
## Règles fermes

 * Aucun résultat de compilation (dll, jar, ...)
 * Aucun fichier spécifique à un ordinateur (préférences, lien d'accès à une base de données, ...)
 * Les fichiers à exclure doivent être **ignorés** (svn:ignore, .hgignore, .gitignore)


# Fichiers à exclure
## Règles négociables

 * Aucun executable ou limiter les fichiers binaires.
 * Limiter les librairies externes (privilégier si possible les outils comme composer, gradle, bower, maven, ...)


# Validation (commit)
## Respecter l'équipe

 * Avant un commit, il faut rafraichir sa copie locale (récupérer les modifications des collaborateurs).
 * Avant de faire un commit, les modifications doivent être testées (par le développeur et via des tests unitaires le cas échéant).
 * Un commit doit avoir un message explicite en bon français.


## Garder la cohérence

 * Un commit ne mélange pas le fond et la forme.
 * Un commit = Un objectif.
 * La suppression ou le renommage se font avec le SCM
 * Les commits doivent être fréquents.
 * Un commit doit être relu.
 * Un commit doit se suffire à lui même.
 * A vous ...


# TOP 8 des pires messages

 * Some shit.
 * It works!
 * fix some fucking errors
 * fix
 * Fixed a little bug...
 * Updated
 * typo
 * Revision 1024!!


# Conflits

 * Ne pas se lancer la patate chaude.
 * Etre adulte.
 * Un conflit n'est pas à cause de l'autre.


# Règles à suivre

 * Avoir des conflits est normal dans un projet.
 * Règles définies = Moins de conflits.
 * Résoudre un conflit nécessite une reflexion.
 * Si votre SCM détecte un conflit, alors sans SCM, il y aurait eu de la perte de code.



# Le meilleur du pire

[Critiquez](https://github.com/seblucas/BadPractice)



# Git / Avancé


# TP / Rebase

# TP / stash



# Travis
