# Space Invader - Sprint 0 : Installation du socle Technique


Commençons par préparer le socle technique nécessaire au bon développement de notre projet.  
Le projet **`spaceinvaders`** sera donc :    
- un [projet maven](#creerProjetMaven)      
- utilisant [git comme gestionnaire de version](#versionnerAvecGit)    
- qui sera [déposé sur Github](#deposersurGithub)    

## Créer un projet maven : `spaceinvaders` <a id="creerProjetMaven"></a>

Si ce n'est pas déjà fait, [créer un projet maven](https://github.com/iblasquez/Back2Basics_Developpement/blob/master/CreerProjetMavenEclipse.md) avec un archetype `maven-archetype-quickstart` que vous appellerez **`spaceinvaders`** avec **`fr.unilim.iut`** comme `group id` et **`spaceinvaders`** comme `artifact id`.

Configurer le `pom.xml` comme indiqué [ici](https://github.com/iblasquez/Back2Basics_Developpement/blob/master/CreerProjetMavenEclipse.md) afin d'utiliser les dernières versions de Java et Junit (voir [ici](https://github.com/junit-team/junit4/wiki/Download-and-Install)).

Si vous avez créé votre projet depuis Eclipse, supprimer également les fichiers créés par défaut`App.java` et `AppTest.java` pour disposer d'un **projet vide** (sans code)...


## Mettre en place le versionning avec git en local sur le projet `spaceinvaders` <a id="versionnerAvecGit"></a>

Pour versionner votre projet spaceinvaders sous git **en local** vous devez suivre les étapes suivantes :

* Créer un dépôt git local sur un projet existant  
* Mettre à jour le fichier `.gitignore`  
* Effectuer un premier commit  
* Visualiser les commits

### 1. Créer un dépôt git local sur un projet existant

Pour cela, vous pouvez utiliser la ligne de commande **`git init`** en vous plaçant à la racine du répertoire contenant le projet **`spaceinvaders`** ou bien utiliser le plug-in git de votre IDE.
  
*Si vous êtes sous Eclipse*, git est géré **[EGit - Git](https://marketplace.eclipse.org/content/egit-git-integration-eclipse)**, un plug-in intégré par défaut à l'IDE.  
Pour transformer le projet **`spaceinvaders`** en **dépôt local git**, il suffit alors d'utiliser **`Team->Share project`** comme indiqué en détail dans le [Tutoriel de découverte de Git (au travers d'EGit)](https://github.com/iblasquez/tuto_git/blob/master/egit/git_egit_tutoriel.md) ou plus succintement dans le [mémo egit](https://github.com/iblasquez/tuto_git/blob/master/egit/git_egit_memo.md) et dont les étapes sont reprises ci-dessous :

* Depuis la vue `Package Explorer`, depuis le projet **spaceinvaders** clic droit  : `Team -> Share project `

* Choix de l'emplacement du dépôt git (pour spaceinvaders, ce sera directement dans le projet **spaceinvaders**) :  
	   -> Cocher **`Use or create repository in parent folder of project`**  
	   -> Vérifier la présence du projet dans la fenêtre  
	   -> Cliquer sur **`Create Repository`** (une fois cliqué cette case doit se regriser  -> puis cliquer **`Finish`**.  


* Depuis la **vue `Package Explorer`**, vérification de la mise en place du gestionnaire de versions : **`spaceinvaders [spaceinvaders master]`** 

### 2. Mettre à jour le fichier `.gitignore`

Certains répertoires et/ou fichiers n'ont pas besoin d’être versionnés, et ne doivent pas être trackés(fichiers de log, fichiers résultants d’une compilation, fichiers de configuration, ...).  
Ces derniers sont à spécifier dans un fichier `.gitgnore` à la racine du dépôt.
Ainsi, non trackés par git, ces fichiers ne seront pas détectés comme ayant subi un changement et ne seront potentiellement commitable.


Le fichier `.gitgnore` dépend donc de l'IDE et de la structure des projets.  
Sous Eclipse, ce dernier ressemblera à quelque chose comme :


``` 

	# Eclipse
	.classpath
	.project
	.settings/

	# Maven
	target/

``` 

`# Eclipse` est un commentaire (optionnel). Sont indiqués ensuite les fichiers et le répertoire de configuration d'Eclipse que nous ne souhaitons pas soumettre au gestionnaire de version (`.classpath` , `.project` et `settings/`).

Outre ces fichiers, il est d'usage d'exclure du gestionnaire de version le répertoire `target/` dans le cadre d'un projet Maven qui contient entre autres les classes compilées de notre projet. Ce répertoire peut être reconstitué à partir du code source.

*Remarque :* Ce fichier vise bien sûr à être personnalisé en fonction des données pertinentes à versionner : `.metadata/`, `*.log` ou autres pourront être ajoutés selon vos besoins (en fonction du type de projet, du depôt git, de l'IDE, ... sur lesquels vous travaillez).   


Sous IntelliJ, il sera plutôt de la forme :


``` 

	# Intellij
	.idea/
	*.iml
	*.iws

	# Maven
	target/


``` 



*Si vous êtes sous Eclipse*, il est facile via l'IDE de configurer le fichier `.gitignore `.  
Placez-vous sur le projet `spaceinvaders`, puis à partir du menu en haut de votre IDE, sélectionnez **`Window -> Show View -> Navigator `**. Un onglet `Navigator` apparait. En se positionnant sur le projet `spaceinvaders`, cette vue permet de visualiser, entre autres, trois fichiers cachés : 
   
* `.project` et `.classpath` qui sont des fichiers techniques gérés par Eclipse 
* `.gitignore` qui est un fichier technique utilisé par Git pour spécifier les fichiers et répertoires à ne pas prendre en compte dans la gestion des versions (c-a-d qui ne seront pas versionnés).  

Depuis la vue `Navigator`, cliquez sur **`.gitignore `** pour ouvrir le fichier.  
Ce fichier contient pour l'instant **`/target/`** ce qui signifie que les fichiers contenus dans le répertoire **`target`** (répertoire où on trouvera entre autres les fichiers byte code `.class`) ne seront pas soumis au gestionnaire de version.

Pour indiquer dans le fichier **`.gitignore`** que le fichier **`.classpath`** ne doit pas être soumis au gestionnaire de version, il suffit depuis la vue **`Navigator`** de se placer sur **`.classpath`**, puis à l'aide d'un clic droit choisir **`Team -> Ignore`**.  
La ligne **`/.classpath`** est alors ajouté dans le fichier **`.gitignore`**.  
Dans la vue  **`Navigator`** une icône avec une croix apparaît devant le fichier **`.classpath`**. 

De la même manière, faites-en sorte que le fichier **`.project`** soit ***`Ignore`***.  
De la même manière, faites-en sorte que le répertoire **`.settings`** soit ***`Ignore`***.  
De la même manière, faites-en sorte que le fichier **`.gitignore`** soit ***`Ignore`***.

Arrivé à cette étape, le contenu de votre fichier **`.gitignore`** doit ressembler à :

``` 
 
	/target/
	/.classpath
	/.project
	/.settings/  
	/.gitignore
   
```

Remarque : Si vous le souhaitez, vous pouvez ajouter les commentaires `# Eclipse` et `# Maven` dans votre fichier `.gitgnore` afin que son contenu ressemble désormais à :


``` 
   
	# Maven
	/target/

	# Eclipse
	/.classpath
	/.project
	/.settings/  
    /.gitignore

   
```


***N'oubliez de sauvegardez le fichier `.gitignore` avant de continuer !***

 
Pour en savoir plus sur comment personnaliser le fichier **`.gitignore `** ...  
- [La rubrique gitignore dans la documentation de git](https://git-scm.com/docs/gitignore#_pattern_format)  
- [A collection of useful .gitignore templates](https://github.com/github/gitignore)    
- [A .gitignore file for Intellij and Eclipse with Maven](http://gary-rowe.com/agilestack/2012/10/12/a-gitignore-file-for-intellij-and-eclipse-with-maven/)  *  
  

### 3. Effectuer un premier commit (`Team -> Commit... `)

Si votre `.gitignore` a bien été complété et enregistré, le premier commit ne devrait concerné que le `pom.xml`. Par convention, vous appelerez ce premier commit **`commit initial`**
Vous pouvez commiter en ligne de commande ou via l'IDE.

*Si vous êtes sous Eclipse*, pour effectuer un premier commit, il suffit de revenir sur la vue `Package explorer` de se positionner sur le projet (`spaceinvaders`), puis d'un clic droit de sélectionner **`Team -> Commit... `**


Une fenêtre s'ouvre. Elle permet de configurer le commit :

* Tout d'abord, en saisissant le **message** qui explicitera la teneur du commit. 
Par exemple : `commit initial`.
* Ensuite, en indiquant l'**auteur** des modifications et la personne qui les a commitées (**committer**) : avec Git, il n'y a pas de commit anonyme (indiquez votre adresse mail).
* Et enfin, en choisissant le(s) fichier(s) à commiter parmi la liste des fichiers proposés (comme il s'agit du premier commit : nous choisirons le `pom.xml` que vous ferez passer de la case ***Unstage Changed*** à la case ***Staged Changes***.  

Validez le commit en appuyant sur `Commit`.


Jetez alors un petit coup d'oeil dans la vue `Package Navigator`, le fichiers `pom.xml` est désormais précédé d'une icône en forme de **cylindre orange**, ce qui signifie que ce fichier est désormais sous contrôle du gestionnaire de version.  


*Remarque : Vous pouvez jetez un petit coup d'oeil [ici](https://github.com/pierreroth64/git-style-guide), c'est un guide de style git qui vous en dira notamment plus sur comment bien nommer vos commit et vos messages de commit.*



### 4. Visualiser les commits

Pour visualier les commits, vous pouvez utiliser la ligne de commande **`git log`** et vous pouvez également visualiser les commits directement sous l'IDE et/ou même avec un outil du genre GitKraken.

 
*Si vous êtes sous Eclipse*, depuis la vue `Package Explorer`, clic droit **`Team -> Show in History `** pour ouvrir la **vue `History`**.  
La vue `History` s'ouvre. Elle permet de visualiser graphiquement l'ensemble des commits et leur message (ou plutôt le titre du message).

*Remarque : pour visualiser plusieurs branches (bouton en haut à droite **Show all branches**)*




## Connecter un dépôt distant existant (type Github) au dépôt local (dans votre IDE) <a id="deposersurGithub"></a>


Nous allons expliquer comment créer un dépôt **`spaceinvaders`** sur Github qui vous servira de **dépôt distant**  
Remarque : Vous pouvez tout aussi bien créer votre dépôt distant (remote) sur GitUnilim, ou GitLab ou autre à la place de Github ;-)


### 1. Créer un compte (sur Github)

Commencez par créer un compte Github si vous n'en avez pas déjà un à partir du lien suivant : [http://github.com/join](http://github.com/join).  
  
En tant qu'étudiant, vous pouvez profiter de l'offre Github Education pour bénéficier de dépots privés et d'autres ressources. Une fois votre compte Github créé, rendez-vous sur [https://education.github.com/](https://education.github.com/) pour profiter de cette offre.


### 2. Créer un dépôt distant (sur Github)

Créez un nouveau dépôt sur Github en suivant la procédure décrite dans la [section **Create a new repository on GitHub** de la page **Create A Repo**](https://help.github.com/articles/create-a-repo/).  
Remplissez juste le **`Repository name`** avec **`spaceinvaders`** et cliquez sur le bouoton  **Create Repository** c-a-d :  
  
* Ne pas cocher Initialize this repository with a *README*
* Ne pas ajouter de *gitignore*
* Ne pas ajouter de *license*

Une fenêtre **Quick setup — if you’ve done this kind of thing before** s'ouvre.
Elle indique l'**URL HTTPS** de votre dépôt (https://github.com/username/spaceinvaders.git où username est votre pseudo GitHub) et des lignes de commande git dont nous allons nous resservir très vite ... Ne toucher à rien pour le moment.


### 3. Connecter le dépôt distant (Github) au dépôt local (celui créé sous votre IDE)

Sous Eclipse, il est possible de connecter le dépôt distant au dépôt local avec le plug-in egit, cette manipulation est indiquée en détail dans le [Tutoriel de découverte de Git (au travers d'EGit)](https://github.com/iblasquez/tuto_git/blob/master/egit/git_egit_tutoriel.md) et reprise plus succintemenet dans le [mémo associé](https://github.com/iblasquez/tuto_git/blob/master/egit/git_egit_memo.md).  
Mais cette manipulation étant un peu **lourde** à mettre en place, nous allons plutôt connecter le dépôt distant et le dépôt local à l'aide des lignes commandes (process qui pourra également être utilisé si vous n'utilisez pas Eclipse ;-)

Si ce n'est pas déjà fait, ouvrez une console pour pouvoir taper les lignes de commande de git (sous Windows, pour manipuler git, mieux vaut utiliser la console git Bash).


Dans la console git, placez-vous dans le répertoire **`spaceinvaders`**.

Revenir sur la page github de votre dépôt **spaceinvaders**, la rubrique 
**…or push an existing repository from the command line** vous indique les deux instructions que nous allons utiliser maintenant :

* recopier (ou taper) dans la console, la première instruction qui permet de connecter votre dépôt local à votre dépôt distant. Cette instruction est de la forme (avec votre propore username) : **`git remote add origin https://github.com/username/spaceinvaders.git**`

* recopier (ou taper) dans la console, la seconde instruction qui permet de pousser le code en local vers le dépôt distant : **`git push -u origin master`**

Consulter sur github, le contenu de votre dépôt **spaceinvaders**, il doit maintenant contenir le fichier **pom.xml**.

Nous venons de pousser des données vers le remote (**`push`**), essayons maintenant de tirer des données du remote (**`pull`**), mais avant cela effectuons une petite modification sur le dépôt distant...

Cliquez sur le bouton vert **add a README**, ne changez rien à la fenêtre qui s'ouvre et cliquez sur **Commit New File**. Bravo vous venez de faire un deuxième commit ;-)
Maintenant, il va falloir resynchroniser le dépôt local avec le déppôt distant.

Recopier (ou taper) dans la console, l'instruction : **`git pull origin`**

Retourner sous Eclipse, vous devriez voir un README qui s'est ajouté dans votre projet ;-)

Votre projet **`spaceinvaders`** est maintenant prêt pour le suite du mini-projet !

Remarques :   
- Pour avoir plus de détail sur la mise en place de git sur un projet Eclipse, vous pouvez en vous aider du [Tutoriel de découverte de Git (au travers d'EGit)](https://github.com/iblasquez/tuto_git/blob/master/egit/git_egit_tutoriel.md) et/ou du [mémo associé](https://github.com/iblasquez/tuto_git/blob/master/egit/git_egit_memo.md).  
- Pour personnaliser vos messages de commit avec des emojis, vous pouvez vous jeter un petit coup d'oeil à ce guide : [An emoji guide for your commit messages](https://gitmoji.carloscuesta.me/)


### 4. Ajout de collaborateurs

Nous allons maintenant ajouter des **collaborateurs** à votre dépôt.    
Pour cela, rendez-vous sur votre dépôt Github et cliquez sur **`Settings`**.  
Choisissez **`Manage access`** (Github va peut-être vous demander de resaisir votre mot de passe).  
Cliquez sur le bouton **Invite a collaborator**.  
Dans le champ `Search by username, full name or email address`, tapez `iblasquez` puis cliquer sur `Add ...`. Vous venez de m'ajouter en tant que collaborateur de votre dépôt :smile: !
  
Ajoutez également, via son identifiant Github ou son adresse email, votre binôme ET votre enseignant de TP.


## Le workflow le plus simple pour commencer
Un des buts de ce mini-projet est de vous permettre de prendre la *bonne* habitude de versionner votre code.

Vous pouvez effectuer vos commits comme vous le souhaitez :  
* depuis l'IDE  
* en ligne de commande  
* via un outil plus visuel de type [GitKraken](https://www.gitkraken.com/)

**La règle à respecter est que les commits soient fréquents et que les messages de commit soient explicites !**

Remarque : Dans le cadre du module M2104, comme vous travaillerez seul sur ce projet et  comme vous faites vos premiers pas avec un gestionnaire de versions, vous adopterez,  dans une premier temps, le workflow le plus simple possible (pas de branche, juste des commits dans la branche principale `master` avec un *tag* sur le dernier commit en fin de séance).   
Toutefois, pour ceux qui sont déjà familarisés avec un gestionnaire de version, il est plutôt conseillé de développer une fonctionnalité par branche et fusionner ensuite dans *master*.


## Déposer sur Github <a id="deposersurGithub"></a>


Vous pousserez votre code fonctionnel en fin de chaque séance de TP sur sur un dépôt github privé (ou public si le coeur vous en dit).

Vous pouvez pousser votre code comme vous le souhaitez :  
* depuis l'IDE  
* en ligne de commande  
* via un outil plus visuel de type [GitKraken](https://www.gitkraken.com/)

Une bonne habitude serait également de tirer votre code en début de séance. 
Cela permettra de s'assurer que le code en local et le code distant est bien synchronisé et vous évitera certainement de mauvaises surprises à la fin de la séance ;-)


### Continuez par le [Sprint 0 : Rapide analyse du problème](SpaceInvaders_S0_QuickDesignSession.md)

