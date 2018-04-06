# Space Invaders - Spike : Prise en main et intégration d'un moteur graphique

***Les documents utilisés dans ce spike et destinés à mettre en place un moteur graphique simplifié (code et documentation) ont été écrits par [Vincent Thomas](https://members.loria.fr/VThomas) pour des étudiants de l'IUT Informatique de Reims.  
Nous les reprenons ici avec l'aimable autorisation de l'auteur.***

**Spike** est un terme agile qui désigne un espace de temps dans un sprint consacré à mener des travaux d'étude, d'exploration technique (pour en savoir plus, vous pouvez jeter un petit coup d'oeil [ici](http://www.aubryconseil.com/post/2008/03/15/387-des-spikes-dans-les-sprints) et/ou [là](http://agiledictionary.com/209/spike)).  
Nous consacrerons ce spike à la prise en main d'un moteur graphique simplifié et à son intégration dans notre jeu. 


Dans le cadre du module M2104, nous avons choisi d'utiliser un moteur graphique simplifié pour faciliter la gestion du jeu, de l'interface homme machine (vous avez le module M2105 qui traite de ce point là : c'est d'ailleurs grâce à ce module que vous devriez facilement pouvoir comprendre et prendre en main le code qui vous est proposé dans ce spike :smile:), la gestion du temps...  
Idéalement, ce moteur doit vous permettre de ne pas avoir a créer de fenêtre, ni à vous occuper des tâches récurrentes que réalise tout moteur de jeu : charger une image, écouter les évènements clavier, mettre à jour les objets du jeu à une certaine fréquence, afficher les objets du jeu sans scintillement, etc...  
Il existe bien sûr de vrais moteurs graphiques plus ou moins légers comme [LIGBX](https://libgdx.badlogicgames.com/), mais leur prise en main nécessite un peu plus de temps et l'objectif de ce mini-projet doit rester centré sur l'apprentissage de l'approche TDD, non sur l'étude d'un moteur graphique :smile:  


Quoi qu'il en soit, dans la vraie vie, vous serez amené à utiliser le code écrit par d'autres développeur et à l'intégrer à votre propre code. C'est le moment de vivre une telle expérience !


**L'objectif** de ce spike est donc d' **intégrer le moteur graphique à votre projet de Space Invaders** et d'en comprendre son fonctionnement.

Pour réaliser cet objectif nous allons passer par les étapes suivantes, à savoir :  
- [Récupérer l'API du moteur graphique dans un projet test](#recupererAPIMoteurGraphique)    
- [Prendre connaissance du code et comprendre le fonctionnement du moteur graphique](#fonctionnementMoteurJeu)     
- [Intégrer le moteur graphique au jeu Space Invaders](#integrationSpaceInvaders)  
- [Tester la *bonne* intégration du moteur graphique (Et bien, jouons maintenant !)](#testAcceptance)  
- [Améliorer l'eXperience Utilisateur](#eXperienceUtilisateur)
   

## Récupérer l'API du moteur graphique dans un projet test <a id="recupererAPIMoteurGraphique"></a>

Dans un premier temps, vous devez importer cette nouvelle API dans un projet test pour commencer à vous familiariser avec son code et son comportement.

Commencez par télécharger le fichier `TD16_moteurGraphique.zip` disponible [ici](ressources/TD16_moteurGraphique.zip) dans le répertoire [ressources](ressources/) de ce dépôt.

Créez ensuite sous Eclipse un **simple projet Java** (clic droit, puis `New -> Java Project`) que vous appelerez **`testmoteurgraphique`**.

Depuis la vue `Package Explorer` via un clic droit, choisissez **`Import -> Archive File`** puis `next` :  

* dans la rubrique **`From Archive File`** indiquer le chemin du fichier que vous venez de telecharger.
	* Dans la case de droite, une case cochée devrait apparaître, dans celle de gauche une classe `Main`
	* dans la rubrique **`Into Folder`** doit se trouver le nom du projet `testmoteurgraphique` (sinon compléter la).
*   cliquer sur `Finish` pour terminer l'import.

Ouvrir le projet `testmoteurgraphique` et remonter les dossiers `monJeu`, `moteurJeu` et la classe `Main` dans `src`. Les packages  `monJeu`, `moteurJeu` apparaissent désormais dans `src`.

Lancer l'application (comme d'habitude via un `Run As -> Java Application` sur la classe `Main`).
Une fenêtre doit s'ouvrir avec une balle bleue au milieu !


Cette balle peut se déplacer via votre interaction au clavier. Pour savoir comment, jetons un rapide coup d'oeil au code ...  
Tout d'abord, rendez-vous dans la méthode `keyPressed` de la classe `keyPressed` pour découvrir quelle touche correspond à quel déplacement (*[magic number](https://sourcemaking.com/refactoring/replace-magic-number-with-symbolic-constant)* ? une constante aurait surement était plus pratique, vous tenterez d'y repenser si vous décidez de refactorer ce code un peu plus tard...).  
La méthode `evoluer` de la classe `MonJeu` vous renvoie vers la méthode `deplacer` de la classe `Personnage` (la balle) qui indique dans son code que seuls deux déplacements sont possible pour ce type de personnage. Quels sont-ils ? Testez-les avec les touches que vous avez identifiées précédemment.


## Prendre connaissance du code et comprendre le fonctionnement du moteur graphique  <a id="fonctionnementMoteurJeu"></a>

### 1. A l'aide du diagramme de classes pour mieux visualiser l'architecture du projet 

A l'aide d'[Object Aid UML Explorer](http://www.objectaid.com/), créez un diagramme de classes (`New -> Other... -> ObjectAid UML Diagram -> Class Diagram`) et drag & droppez-y les classes du package `moteurJeu` pour commencer.

Vous pouvez ensuite ajouter les classes du package `monJeu`.


### 2. A l'aide de la documentation fournie

La documentation de cette API est consultable dans le fichier suivant `TD16_COO_Zeldiablo_moteurGraphique` disponible [ici](ressources/TD16_COO_Zeldiablo_moteurGraphique.pdf) dans le répertoire [ressources](ressources/) de ce dépôt.

Téléchargez et ouvrez ce fichier.  
Lisez la partie **1. Moteur de Jeu Générique** pour comprendre le fonctionnement général du moteur.   
Lisez la partie **3. Annexe : Fonctionnement interne du moteur de jeu** pour comprendre le fonctionnement interne du moteur.  
Ne lisez pas la partie 2 !
  
**Ne pas hésitez à faire des allers-retours entre le texte et le code**.  
Lors de la lecture du **diagramme de séquence** notamment, suivez pas à pas l'enchainment des interactions dans le code pour une meilleure compréhension du moteur !


## Intégrer le moteur graphique au jeu Space Invaders <a id="integrationSpaceInvaders"></a>

Maintenant que vous avez pris en main cette nouvelle API, il est temps d'intégrer et d'adapter ce code à notre projet pour pouvoir disposer via ce moteur d'un rendu graphique temps réel.

### 1. Integration du code du moteur dans notre Space Invaders

Intégrer le code du moteur graphique à notre projet revient, dans un premier temps, à créer sous `src/main/java`, un nouveau package **`fr.unilim.iut.spaceinvaders.moteurjeu`** et à copier/coller les classes du package `moteurJeu` dans ce nouveau package.

Il faut ensuite adapter le moteur graphique et prendre les dispositions qui s'imposent pour qu'il puisse fonctionner correctement dans notre projet.

### 2. Adaptation du moteur graphique à notre Space Invaders

D'après la documentation et notamment les parties **1.1 Description des classes du moteur** ,  **1.3 Utilisation du moteur** et l'**annexe:** pour adapter ce moteur graphique à un nouveau jeu, il est necessaire de créer au moins **deux classes** qui implémentent les deux interfaces suivantes :  
- l'interface `Jeu` et plus particulièrement la méthode `void evoluer(Commande commande)`.  
- l'interface `DessinJeu` et plus particulièrement la méthode `void dessiner(BufferedImage image)` qui a pour objectif de dessiner l'image du jeu sur l'image du jeu passé en paramètre `image`  
Pour disposer d'une application graphique et pouvoir lancer le moteur graphique, il nous faut une méthode `main`. Vous créerez donc également **une nouvelle classe** `Main` dédiée au lancement du moteur et qui implémentera `main` :smile:  
(Astuce : Si vous écrivez `main` suivi d'un `CTRL+ESPACE` l'auto-complétion d'Eclipse vous proposera directement la signature d'un `main` :smile: ).

Voici quelques conseils supplémentaires qui devraient vous permettre d'intégrer plus facilement le moteur graphique en vous aidant de la documentation et du code de l'exemple : 

*  La **classe `SpaceInvaders`** n'est autre que la classe de `MonJeu` de l'exemple de code précédent, celle qui va *contrôler* le jeu (en connaître ses règles) et déclarer les *personnages* du jeu.  
Vous devez donc tout mettre en oeuvre pour que la classe `SpaceInvaders` implémente l'interface `Jeu` et qu'elle rédéfinisse correctement les méthodes `evoluer` et `etreFini` en tenant compte des besoins actuels de notre jeu Space Invaders (déplacement du vaisseau possible uniquement de droite à gauche et jeu infini). Il est intéressant de noter pour la suite, ce que nous indique la partie 1.3 de la documentation, c-a-d que c'est *la méthode `evoluer` qui encapsule les règles du jeu*.
 
* Une **nouvelle classe `DessinSpaceInvaders`** doit ensuite être créée dans votre projet.  
	* Cette classe a pour but *de dessiner l'image du jeu* : elle doit implémenter l'interface `Jeu` et donc redéfinir la méthode `void dessiner(BufferedImage image)` dont le seul objectif est, dans l'état actuel de votre Space Invaders, de dessiner un vaisseau rectangulaire (à l'aide de la méthode `fillRect` comme dans l'exemple de code) de couleur grise par exemple.  
	***Remarques concernant l'affichage :***  
    -> L'affichage se fera directement en pixel, nous n'utiliserons pas de constante **`TAILLE_CASE`** !
	-> une méthode `dessinerdessinerObjet` comme dans l'exemple est-elle vraiment nécessaire ?  
    -> **ATTENTION !!!**  
    **L'origine du rectangle dessiné par `fillRect` et l'origine du `Vaisseau` sont différents !!!**   
	En effet, la javadoc de la classe Graphics disponible [ici](https://docs.oracle.com/javase/7/docs/api/java/awt/Graphics.html) indique à propos de la méthode `fillRect` :  
 	`public abstract void fillRect(int x,int y, int width, int height)`  
	*Fills the specified rectangle. The left and right edges of the rectangle are at x and x + width - 1. The top and bottom edges are at y and y + height - 1. The resulting rectangle covers an area width pixels wide by height pixels tall. The rectangle is filled using the graphics context's current color.*  
	Ainsi le `x` de la méthode `fillRect` repésente l'*abscisse la plus à gauche* et le `y` de la méthode `fillRect` repésente l'*ordonnée  la plus *basse** c-a-d les coordonnées du coin gauche **supérieur** du rectangle à dessiner si l'axe des abscisses est vers la gauche et l'axe des ordonnées vers le bas, alors que que les coordonnées `x` et `y` de la `Position` `origine` d'un objet de type `Vaisseau` correspond aux coordonnées du coin gauche **inférieur**.  
	***Soyez malin et utilisez les méthodes déjà existantes dans la classe `Vaisseau` pour récupérer facilement les *bonnes* coordonnées :smile: !***  
	
  
	* De plus, comme dans le code exemple de la classe `DessinJeu` (classe équivalente à `DessinSpaceInvaders`), votre classe `DessinSpaceInvaders` devra disposer d'un attribut de type `SpaceInvaders` et donc d'un constructeur à un paramètre de type `SpaceInvaders` : ceci pour permettre à *votre classe*  `DessinSpaceInvaders` de connaitre *votre jeu* `SpaceInvaders` et de l'afficher lorsque le moteur le demande (cf. partie 1.3 de la documentation).  


* Une **nouvelle classe `Main`**  doit également être créé pour pouvoir disposer d'une application graphique c-a-d permettre au moteur de lancer le jeu.  
A l'image de la classe `Main` de l'exemple et d'après la documentation (cf. partie 1.2 Description du fonctionnement du moteur), cette classe doit disposer d'un objet `jeu` de type `SpaceInvaders` et d'un objet `afficheur`de type `DessinSpaceInvaders`.   
Ces deux objets sont nécessaire pour créer le `MoteurGraphique`.
Avant de créer le `MoteurGraphique`, vous devriez peut-être faire en sorte que le `jeu` appele **une nouvelle méthode `initialiserJeu`** (qui n'aura pas d'impact sur les tests déjà écrits). Cette méthode, à écrire dans la classe `SpaceInvaders`, pourrait par exemple dans une premier temps positionner un vaisseau au milieu en bas de votre écran : smile:  
Une fois le jeu initialisé, le moteur peut être créé et une fois créé, le `moteur` peut lancer le jeu en passant en paramètre la taille de l'écran.  
Pour faciliter le paramétrage du jeu, utilisez des **constantes** comme indiqué ci-après :smile:   
En effet, La taille de l'écran, (définie lors de l'appel de la méthode `lancerJeu(int width, int height)`)  et la taille de l'espace de jeu (définie lors de l'appel du constructeur `SpaceInvaders(int longueur, int hauteur)`) doivent être les mêmes (puisque nous n'avons pas souhaité gardé la constante **`TAILLE_CASE`** dans la classe permettant le dessin).
Pour faciliter la manipulation et le paramétrage de ces données, nous allons les regrouper sous forme de constantes au sein d'une même classe.  

* Créez donc une **nouvelle classe `Constante`**.   
Commencez par ajouter dans cette classe, les deux constantes qui vont permettre de paramétrer la taille de l'espace jeu (et donc aussi de l'écran) et seront appelées dans la classe `Main`.
Continuez en ajoutant deux autres constantes qui vont permettre de paramétrer les dimensions du `Vaisseau` et devront être appelées dans la nouvelle méthode `initialiserJeu`.
Pour tester la *bonne* intégration du moteur, vous pouvez par exemple prendre comme valeurs pour les constantes : 

```JAVA

    public class Constante {

	    public static final int ESPACEJEU_LONGUEUR = 150;
	    public static final int ESPACEJEU_HAUTEUR = 100;
	
	    public static final int VAISSEAU_LONGUEUR = 30;
	    public static final int VAISSEAU_HAUTEUR = 20;
   }

```



A vous de jouer maintenant !  
En tenant compte des remarques précédentes, adaptez par vous-même le moteur graphique à votre projet.

Une fois les classes **`SpaceInvaders.java`**, **`DessinSpaceInvaders.java`**, **`Vaisseau.java`**, **`Main.java`** et **`Constantes.java`** correctement implémentées vous devriez pouvoir lancer une application graphique et interagir avec votre vaisseau :smile: ...

... Toutefois, si vous aviez des difficultés à adapter et à lancer le moteur graphique dans votre projet Space Invaders, une implémentation possible détaillée est proposée [ici](SpaceInvaders_Spike_MoteurGraphique_UneAdaptationPossible.md) : mais vous devez d'abord chercher par vous-même avant d'y jeter un coup d'oeil !


### 3. Un peu de refactoring ?

Vous venez de créer une **classe `Constante`**. 
Pourquoi ne pas y déplacer les constantes déjà déclarées dans votre application ?

Si vous passez en revue toutes les classes déjà écrites, vous constaterez que seule la classe `SpaceInvaders` dispose actuellement de constantes.  
Il ne vous reste donc plus qu'àtransférer ces constantes vers la classe `Constante` en vous aidant de l'IDE.

Pour cela, commencez pas passer ces constantes de `private` en `public` et n'oubliez pas d'enregistrer !

Sélectionnez pour commencer `MARQUE_FIN_LIGNE`, puis à l'aide d'un clic droit, choisissez `Refactor -> Move` et dans la destination indiquez `Constante`, terminez en cliquant sur `OK`.   
Et voilà, le tour est joué ! La constante `MARQUE_FIN_LIGNE` a été déplacée dans la classe `Constante` et l'IDE a automatiquement mis à jour les appels à cette constante puisque vous avez fait appel à une fonction de refactoring de l'IDE :smile:

Faites de même avec les deux autres constantes `MARQUE_VIDE` et `MARQUE_VAISSEAU`.

> **Vous venez de faire des modifications dans votre code...**  
> ***N'oubliez pas de relancer les tests pour vérifier que le comportement de votre code n'a pas changé !***


## Tester la *bonne* intégration du moteur graphique (Et bien, jouons maintenant !) <a id="testAcceptance"></a>

Il faut maintenant tester le *bon* fonctionnement de l'application SpaceInvaders que vous venez de créer et voir si les fonctionnalités développées jusqu'à présent se comportent bien selon les exigences (*du client*) c-a-d si tous les critères d'acceptance des différentes fonctionnalités peuvent bien être validés.

Voici donc venu le temps de procéder à vos premiers tests d'acceptance (au niveau *produit*) en tant qu'utilisateur de votre produit.

Contrairement aux tests unitaires (au niveau *code*) que vous avez automatisés lors du développement grâce à l'approche TDD, vous allez maintenant exécuter ces tests d'acceptance de manière manuelle c-a-d en interagissant vous même directement avec votre application (via le clavier) une fois que votre jeu sera lancé !

Comme vous n'avez pas vraiment écrit de protocole de tests, vous allez faire ce que l'on appelle des [tests exploratoires](http://institut-agile.fr/exploratory.html).
Vous ferez donc en sorte de vérifier le *bon* comportement des deux fonctionnalités implémentées jusqu'à présent qui doivent permettre de :
- pouvoir dimensionner le vaisseau et
- pouvoir déplacer le vaisseau de droite à gauche sans déborder de l'espace jeu :smile:

Il ne vous reste donc plus qu'à constater que le vaisseau affiché a bien une dimension (cohérente avec la dimension souhaitée) et à effectuer quelques déplacements à l'aide des touches du clavier pour vérifier (et valider) que votre vaisseau peut bien se déplacer vers la gauche, vers la droite et uniquement dans ces deux directions.
Vous n'oublierez pas de tester également les cas limites afin de vérifier que votre vaisseau s'arrête bien quand il arrive en butée à droite et à gauche de l'espace jeu et n'en déborde pas...

Normalement tout devrait bien se passer puisque vous aviez mis en place des tests unitaires automatisés !

A vous de jouer !

Suite aux différentes tests que vous venez d'effectuer sur votre produit, j'aurais une petite question à vous poser : quelle est votre ressenti par rapport à votre application ? N'auriez-vous pas une petite remarque, un petit retour (*feedback*), une proposition à émettre pour rendre plus agréable l'utilisation de ce jeu et améliorer ainsi son *eXpérience Utilisateur (UX)* ?

## Améliorer l'eXperience Utilisateur <a id="eXperienceUtilisateur"></a>


### 1. Améliorer l'eXperience Utilisateur en utilisant les flèches du clavier

Personnellement, je préfère jouer avec les flèches... 

Si c'est pareil par vous, sachez qu'il existe des constantes dans la classe `Key Event` qui permettent de mettre en place facilement ce paramètrage.  
Jetez un petit coup d'oeil [ici](https://docs.oracle.com/javase/7/docs/api/java/awt/event/KeyEvent.html) dans la javadoc de `Key Event` pour consulter ces constantes.  
Vous constaterez par exemple que `VK_LEFT` permet de reconnaitre la touche correspondant à la flèche de gauche (celle du clavier, pas celle du pavé numérique :smile:) et `VK_RIGHT` permet reconnaitre la touche correspondant à la flèche droite du clavier.

En début de ce tutoriel, nous avions vu que les interactions avec le clavier étaient traitées dans les méthodes `keyPressed` et `keyReleased` de la classe `Controleur` du paquetage `fr.unilim.iut.monspaceinvaders.moteurjeu`.

Rendez-vous dans dans cette classes et remplacez donc, dans les deux méthodes (`keyPressed` et `keyReleased`) : `q` et `d` par respectivement `KeyEvent.VK_LEFT` et `KeyEvent.VK_RIGHT`.  
Même si pour l'instant, vous n'utilisez qu'un déplacement horizontal dans votre jeu, pour plus de cohérence dans votre code, profitez-en aussi pour remplacer `z` et `s` par respectivement `KeyEvent.VK_UP` et `KeyEvent.VK_DOWN`

Attention si vous décidez d'utiliser ces constantes, il vous faudra aussi remplacer l'appel à `getKeyChar` par un appel `getKeyCode` switch c-a-d que les `switch (e.getKeyChar())` deviennent des `switch (e.getKeyCode())`.

En supprimant les commentaires et en rajoutant une rubrique `default` dans les `switch`, le code de ces deux méthodes devient :

```JAVA
	
    @Override
    public void keyPressed(KeyEvent e) {

		switch (e.getKeyCode()) {
		case KeyEvent.VK_LEFT:
			this.commandeEnCours.gauche = true;
			this.commandeARetourner.gauche = true;
			break;
		case KeyEvent.VK_RIGHT:
			this.commandeEnCours.droite = true;
			this.commandeARetourner.droite = true;
			break;
		case KeyEvent.VK_UP:
			this.commandeEnCours.haut = true;
			this.commandeARetourner.haut = true;
			break;
		case KeyEvent.VK_DOWN:
			this.commandeEnCours.bas = true;
			this.commandeARetourner.bas = true;
			break;
		default:
			break;
		}
	}

    @Override
	public void keyReleased(KeyEvent e) {
		switch (e.getKeyCode()) {
		case KeyEvent.VK_LEFT:
			this.commandeEnCours.gauche = false;
			break;
		case KeyEvent.VK_RIGHT:
			this.commandeEnCours.droite = false;
			break;
		case KeyEvent.VK_UP:
			this.commandeEnCours.haut = false;
			break;
		case KeyEvent.VK_DOWN:
			this.commandeEnCours.bas = false;
			break;
		default: break;
		}
	}

```


Vous êtes libre de personnaliser votre Space Invaders d'utiliser les touches que vous souhaitez pour interagir avec votre jeu :smile:     
A vous de voir si vous décidez si vous souhaitez interagir par l'intérmédiaire des flèches (avec une détection par un `getKeyCode`) ou par l'intérmédiaire de touches de caractères (avec une détection par un `getKeyCode`).    
Par contre, n'oubliez pas de préciser le *mode d'emploi* sur la manière d'interagir dans votre documentation utilisateur (Dans le cadre du module M2104, cela signifie que cette information doit se retrouver dans votre rapport :smile:). 

Remarque : Et si vous envisagez un jour de mettre en place des [easter egg](https://fr.wikipedia.org/wiki/Easter_egg) dans votre jeu, il se pourrait bien que vous ayiez besoin de revenir rejouer avec ce code là :smile: 


### 2. Améliorer l'eXperience Utilisateur en permettant au vaisseau de se déplacer plus rapidement

Personnellement, j'ai trouvé que le vaisseau se déplacer *trop* lentement (pixel par pixel) ...

Permettre au vaisseau de se déplacer plus rapidement revient à pouvoir régler la vitesse au vaisseau.
Nous venons donc d'identifier ici une nouvelle fonctionnalité à implémenter dans notre projet. La mise en place de cette fonctionnalité fera donc l'objet du sprint suivant puisque ce sprint était un spike uniquement consacré à la prise en main technique du moteur graphique et non au développement de nouvelles fonctionnalités, développement qui, rappelons-le, doit être fait dans une approche TDD :smile:


## Gestion de Version

**Ce spike est désormais terminé et l'intégration du moteur graphique est réussie : il est temps de committer les derniers changements dans votre gestionnaire de version !**

Lors de votre commit, vous devez :

* bien prendre garde à ajouter dans votre index toutes les nouvelles classes qui vous ont permis de mener à bien cette intégration c-a-d toutes les classes du package **`fr.unilim.iut.monspaceinvaders.moteurjeu`**, mais aussi les nouvelles classes telles que **`DessinSpaceInvaders.java`**, **`Main.java`** et **`Constante.java`**.

* Le message du commit pourrait refléter les changements liés à ce spike en mentionnant par exemple : **Intégration du moteur graphique**.


## En savoir un peu plus sur le développement de jeu vidéo...

Développer entièrement un jeu vidéo *from scratch* n'est pas si simple...

Une petite vidéo (15 minutes) :[Développer un jeu vidéo quand on n’y connait rien en développement de jeux vidéo (David Wurste)](https://www.youtube.com/watch?v=4X337M8kU8Q) 

Pour en savoir un peu plus, jetez à l'occasion un petit coup d'oeil sur le site de [Vincent Thomas ](https://members.loria.fr/VThomas) et plus particulièrement dans la rubrique [Tutoriel de Jeux Video en Java](https://members.loria.fr/VThomas/mediation/JV_IUT_2016/). 
<!-- D'autres références dont également disponibles dans la [page Références](../SpaceInVaders_References.md) de ce dépôt. -->

Si vous voulez développez un *vrai* moteur léger pour le développement futur de vos jeux vidéos, vous pouvez vous renseigner sur [LIBGDX](https://libgdx.badlogicgames.com/).   
[*LibGDX is a free and open-source game-development application framework written in the Java programming language with some C and C++ components for performance dependent code. It allows for the development of desktop and mobile games by using the same code base. It is cross-platform, supporting Windows, Linux, Mac OS X, Android, iOS, BlackBerry and web browsers with WebGL support.(Wikipédia)*](https://en.wikipedia.org/wiki/LibGDX).


### Continuez par la [fonctionnalité n° 3 : Choisir la vitesse du vaisseau](SpaceInvaders_S3_ChoisirVitesseVaisseau.md)