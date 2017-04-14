# Space Invader - Sprint 0 : Installation du socle Technique


Commençons par préparer le socle technique nécessaire au bon développement de notre projet.  
Le projet **`spaceinvaders`** sera donc :    
- un [projet maven](#creerProjetMaven)      
- utilisant [git comme gestionnaire de version](#versionnerAvecGit)    
- qui sera [déposé sur Github](#deposersurGithub)    

## Créer un projet maven : `spaceinvaders` <a id="creerProjetMaven"></a>

Si ce n'est pas déjà fait, [créer un projet maven](https://github.com/iblasquez/Back2Basics_Developpement/blob/master/CreerProjetMavenEclipse.md) que vous appellerez **`spaceinvaders`** avec **`fr.unilim.iut`** comme `group id` et **`spaceinvaders`** comme `artifact id`.

Configurer le `pom.xml` comme indiqué [ici](https://github.com/iblasquez/Back2Basics_Developpement/blob/master/CreerProjetMavenEclipse.md) afin d'utiliser les dernières versions de Java et Junit (voir [ici](https://github.com/junit-team/junit4/wiki/Download-and-Install)).

Si vous avez créé votre projet depuis Eclipse, supprimer également les fichiers créés par défaut`App.java` et `AppTest.java` pour disposer d'un **projet vide** (sans code)...


## Versionner avec git<a id="déposersurGithub"></a>

### 1. Mise en place de Git sur le projet spaceinvaders

Si ce n'est pas déjà fait, vous devez également passer le projet **`spaceinvaders`** sous Git.

Pour cela, vous devez suivre les étapes suivantes :

* Transformer le projet **`spaceinvaders`** en **dépôt local git** (**`Team->Share project`**), puis :  
-> configurer le fichier **`.gitignore`**  
-> faire un premier commit contenant **`.gitgnore`** et **`pom.xml`**


* Créer un dépôt sur Github **`spaceinvaders`** qui vous servira de **dépôt distant**


* Connecteur votre dépôt distant (**Remote**) à votre dépôt local en prenant soin pour commencer :  
-> de configurer correctement l'option **`Push` (ROUGE)**  
-> de **pusher** le contenu du dépôt local vers le dépôt distant pour vérifier que l'opération a bien été configurée.


* Se rendre sur le dépôt distant (**sur Github**) afin de :  
-> vérifier que l'opération push a été effectuée correctement, puis   
-> créer (depuis Github) un **`README.md`** qui pourra par exemple contenir : *Implémentation du projet space invaders en TDD à partir de https://github.com/iblasquez/tdd_spaceInvaders*. Pour en savoir un peu plus sur ce que devrait contenir un README, jetez un petit coup d'oeil [ici](https://help.github.com/articles/about-readmes/).  
-> et **committer** l'ajout de ce **`README`**   

* Revenir sous Eclipse afin de :  
-> configurer l'option **`Fetch` (VERT)** de votre Remote  
-> procéder à un **`Fetch`** pour vérifier que l'opération Fetch été configuréé  
-> procéder à un **merge** afin que les données rapatriées puissent fusionner avec les données locales, c.-à-d. que le fichier **`README.md`** apparaisse bien dans le workspace sous Eclipse  

Votre projet **`spaceinvaders`** est maintenant prêt pour le suite du mini-projet !

Remarques :   
- Pour avoir plus de détail sur la mise en place de git sur un projet Eclipse, vous pouvez en vous aider du [Tutoriel de découverte de Git (au travers d'EGit)](https://github.com/iblasquez/tuto_git/blob/master/egit/git_egit_tutoriel.md) et/ou du [mémo associé](https://github.com/iblasquez/tuto_git/blob/master/egit/git_egit_memo.md).  
- Pour personnaliser vos messages de commit avec des emojis, vous pouvez vous jeter un petit coup d'oeil à ce guide : [An emoji guide for your commit messages](https://gitmoji.carloscuesta.me/)


### 2. Ajout de collaborateurs

Nous allons maintenant ajouter des **collaborateurs** à votre dépôt.    
Pour cela, rendez-vous sur votre dépôt Github et cliquez sur **`Settings`**.  
Choisissez **`Collaborators`** (Github va peut-être vous demander de resaisir votre mot de passe).  
Dans le champ `Search by username, full name or email address`, tapez `iblasquez` puis cliquer sur `Add collaborator`. Vous venez de m'ajouter en tant que collaborateur de votre dépôt :smile: !
  
Ajoutez également, via son identifiant Github ou son adresse email, votre binôme ET votre enseignant de TP.


### 3. Le workflow le plus simple pour commencer
Un des buts de ce mini-projet est de vous permettre de prendre la *bonne* habitude de versionner votre code.

Remarque : Dans le cadre du module M2104, comme vous travaillerez juste en binôme sur le même projet et  comme vous faites vos premiers pas avec un gestionnaire de versions, vous adopterez,  dans une premier temps, le workflow le plus simple possible (pas de branche, juste des commits dans la branche principale `master` avec un *tag* sur le dernier commit en fin de séance).   
Toutefois, pour ceux qui sont déjà familarisés avec un gestionnaire de version, il est plutôt conseillé de développer une fonctionnalité par branche et fusionner ensuite dans *master*.


## Déposer sur Github <a id="deposersurGithub"></a>

Vous pousserez votre code fonctionnel en fin de chaque séance de TP sur sur un dépôt github privé (ou public si le coeur vous en dit).


### Continuez par le [Sprint 0 : Rapide analyse du problème](SpaceInvaders_S0_QuickDesignSession.md)

