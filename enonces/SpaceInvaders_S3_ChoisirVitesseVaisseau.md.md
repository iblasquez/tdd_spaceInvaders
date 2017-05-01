# Space Invaders - Sprint 3 : Choisir la vitesse du vaisseau


**L'objectif** de ce sprint est de *pouvoir* **choisir la vitesse du vaisseau** *afin* que le vaisseau puisse se déplacer à une vitesse convenable dans l'application graphique.

<!--[Sprint Backlog](images/spaceinvaders_s3.png)-->


Pour réaliser cet objectif, nous allons ajouter une ***vitesse*** au code existant de la classe `Vaisseau` en prenant soin que ce changement ne vienne pas perturber le comportement actuel (c-a-d que tous les tests écrits jusqu'à présent continuent de bien de passer AU VERT)...

Pour cela, nous allons suivre les étapes suivantes :  
- [Quick Design Session : Comprendre ce qu'est la *vitesse* dans notre application et faire un choix de conception](#choixConceptionVitesse)   
- [Ajouter la `vitesse` au `Vaisseau` sans régression de comportement](#ajouterVitesseSansRegression)  
- [Régler la vitesse du vaisseau](#reglerVitesse)      
- [Faire en sorte que le déplacement se fasse *correctement* pour une vitesse quelconque](#deplacementAUneCertaineVitesse)   
- [Et bien, jouons maintenant !](#testAcceptance) 

sans oublier de ...  
- [Committer les changements liée à cette nouvelle fonctionnalité](#commit)  

 

## Quick Design Session : Comprendre ce qu'est la *vitesse* dans notre application et faire un choix de conception <a id="choixConceptionVitesse"></a>

La vitesse que nous souhaitons implémenter est une *vitesse instantanée* qui d'[après Wikipédia](https://fr.wikipedia.org/wiki/Vitesse) peut être définie comme
[*un vecteur obtenu en dérivant les coordonnées cartésiennes de la position par rapport au temps*](https://fr.wikipedia.org/wiki/Vitesse).

Ainsi dans un espace à deux dimensions, comme celui l'espace de jeu de Space Invaders, la vitesse d'un objet peut-être définie par un vecteur *v* à 2 dimensions (*dx* et *dy*) où  :  
- ***dx*** correspond au **déplacement** (c-a-d à un **nombre de pixels** pour le projet SpaceInvaders) **effectué en 1 unité de temps** sur l'axe des abscisses  
- ***dy*** correspondra au **déplacement** (c-a-d à un **nombre de pixels** pour le projet SpaceInvaders) **effectué en 1 unité de temps** sur l'axe des ordonnées.


A partir de cette première réflexion, quel pourrait-être votre choix de conception pour donner une vitesse au `Vaisseau` ?

* **La solution n°1 (la plus rapide)** consisterait à **ajouter directement comme attributs de la classe `Vaisseau` deux types primitifs entiers `int dx` et `int dy`**... Hmm dans ces conditions, n'est-on pas en train de faire apparaître un code smell de type [Primitive Obsession](https://sourcemaking.com/refactoring/smells/primitive-obsession) ?

* **La solution n°2** consisterait alors à **créer une classe `Vitesse`** composée des deux types primitifs `dx` et `dy` et à ajouter un nouvel **attribut `vitesse` de type `Vitesse` dans la classe `Vaisseau`**...

Mais, intéressons-nous de plus près à notre application Space Invaders et à ces spécificités...
Dans un Space Invaders, les objets qui se déplacent sont le vaisseau, le(s) missile(s) et l'(es) alien(s).
Chacun de ces objets se déplace soit horizontalement, soit verticalement, mais, a priori, jamais en diagonale.  
Cela signifie que ***le déplacement d'un objet dans le cas du Space Invaders se fera uniquement suivant une seule dimension*** (celle des x pour un déplacement dit horizontal, ou celle des y pour un déplacement dit vertical). Dans ces conditions, est-il vraiment nécessaire de disposer d'un vecteur vitesse à 2 dimensions ? ...

En tenant compte de cette dernière remarque et en essayant de rester le plus [YAGNI](https://fr.wikipedia.org/wiki/YAGNI) possible, il semblerait que, pour l'instant, **un simple attribut `vitesse` de type entier** soit suffisant pour représenter la *vitesse* du `Vaisseau` : ce sera notre choix de conception pour la suite.

Peut-être serait-il d'ailleurs intéressant donner une définition de la *vitesse* dans votre glossaire pour en connaître ses limites et sa mesure dans le cadre de votre application... :smile:


## Ajouter la `vitesse` au `Vaisseau` sans régression de comportement <a id="#ajouterVitesseSansRegression"></a>

Il est maintenant grand temps de remettre les mains dans le code !

Relancez les tests pour vous assurer qu'ils passent toujours tous AU VERT !

### 1. Ajouter un attribut `vitesse` à la classe `Vaisseau`

D'après ce qui précéde, commencez à ajouter un attribut entier `vitesse` dans la classe `Vaisseau`.

```JAVA

    public class Vaisseau {

	   private Position origine;
	   private Dimension dimension;
	   private int vitesse;

       //...
   }

```


### 2. Introduire la `vitesse` dans le code existant de la classe `Vaisseau` de manière non-régressive

Lorsqu'on lance l'application graphique, on constate que le vaisseau se déplace déjà à une certaine vitesse.  
Deux questions devraient alors vous venir à l'esprit :  
- Quelle est la valeur de cette vitesse ?  
- Où se *cache* la vitesse dans le code de la classe `Vaisseau` déjà écrit ?

A chaque unité de temps, c'est-à-dire à chaque fois qu'un déplacement est demandé, le vaisseau se déplace actuellement de 1 pixel : **la valeur actuelle de la vitesse est donc de 1.**

Cette vitesse *se cache* dans les **`méthodes seDeplacerVersLaDroite`** et **`seDeplacerVersLaGauche`** où elle apparaît actuellement sous la forme **`+1`** et **`-1`**.

Ce constat fait, vous pouvez intervenir sur le code.

Commencez par remplacer dans les méthodes **`seDeplacerVersLaDroite`** et **`seDeplacerVersLaGauche`**, les **`+1`** et **`-1`** par **`+vitesse`** et **`-vitesse`** de manière à obtenir :

```JAVA

    public void seDeplacerVersLaDroite() {
		this.origine.changerAbscisse(this.origine.abscisse() + vitesse);
	}
    
    public void seDeplacerVersLaGauche() {
		this.origine.changerAbscisse(this.origine.abscisse() - vitesse);
	}

``` 

> **Vous venez de faire des modifications dans votre code...**  
> ***N'oubliez pas de relancer les tests pour vérifier que le comportement de votre code n'a pas changé !***

Et là bing ! les tests sont AU ROUGE !!!  
Ce qui est tout à fait normal puisque nous n'avons pas encore initialisé la valeur de `vitesse` à `1` et que par défaut, elle est à `0` :smile:

Pour faire passer les tests le plus rapidement AU VERT, il suffit donc d'ajouter une instruction (celle de l'initialisation de la vitesse `this.vitesse = 1;`) dans le constructeur suivant :

```JAVA

    public Vaisseau(Dimension dimension, Position positionOrigine) {
		this.dimension = dimension;
		this.origine = positionOrigine;
		this.vitesse = 1;
	}

```

> **Vous venez de faire des modifications dans votre code...**  
> ***N'oubliez pas de relancer les tests pour vérifier que le comportement de votre code n'a pas changé !***

Et là, les tests devraient normalement passer AU VERT !!!

Nous avons donc modifié notre code actuel sans en changer le comportement : pas de régression par rapport à l'existant, puisque les tests sont AU VERT ! 

Par contre, ce code ne fonctionne que pour une vitesse égale à `1`, il est donc maintenant temps de permettre le choix d'une autre valeur de vitesse...


## Régler la vitesse du vaisseau <a id="reglerVitesse"></a>

Choisir la valeur de la vitesse du vaisseau devrait pouvoir se faire :

* lors de la création du vaisseau : en passant en paramètre du constructeur la valeur souhaitée
* ou à n'importe quel moment via un setteur qui permettrait alors de sélectionner une nouvelle vitesse.

Actuellement, nous n'avons pas besoin de modifier la vitesse du vaisseau une fois le jeu lancé (peut-être cela sera-t-il nécessaire *plus tard* lorsque vous envisagerez d'implémenter de nouvelles options dans notre jeu).  
Pour l'instant, seul le réglage de la vitesse du Vaisseau via le constructeur nous est donc utile.

Pour le mettre en place, il suffit d'ajouter un nouveau constructeur à trois paramètres, dont le dernier paramètre correspond à la `vitesse` : 

```JAVA

	public Vaisseau(Dimension dimension, Position positionOrigine, int vitesse) {
		this.dimension = dimension;
		this.origine = positionOrigine;
		this.vitesse = vitesse;
	}

```

Au passage, vous pouvez faire en sorte que le constructeur précédent (à deux paramètres) appelle désormais ce nouveau constructeur en lui passant une vitesse par défaut de `1` :

```JAVA

	public Vaisseau(Dimension dimension, Position positionOrigine) {
		this(dimension, positionOrigine, 1);
	}

```

> **Vous venez de faire des modifications dans votre code...**  
> ***N'oubliez pas de relancer les tests pour vérifier que le comportement de votre code n'a pas changé !***

Les tests doivent continuer de passer AU VERT !  

Remarque : Certes, nous n'avons pas encore écrit de code pour le constructeur à 3 paramètres, mais nous allons l'utiliser dès le prochain test :smile:

## Faire en sorte que le déplacement se fasse *correctement* pour une vitesse quelconque <a id="deplacementAUneCertaineVitesse"></a>

Il est donc temps de reprendre une approche TDD et de tester un nouveau comportement de l'application. Pour commencer, ce sera le déplacement vers la droite...

### 1. Déplacement vers la *droite* pour une vitesse quelconque

#### 1.1 Cas *normal* (et un peu de refactoring au passage)

Prenons l'exemple d'un déplacement *normal* vers la droite d'un vaisseau qui irait à une vitesse de `3`, et qui après son déplacement se trouverait toujours dans l'espace de jeu.
Cet exemple pourrait être illustré par le test suivant : 

```JAVA

    public void test_VaisseauAvance_DeplacerVaisseauVersLaDroite_AvecVitesse() {

       spaceinvaders.positionnerUnNouveauVaisseau(new Dimension(3,2),new Position(7,9),3);
       spaceinvaders.deplacerVaisseauVersLaDroite();
       assertEquals("" + 
       "...............\n" + 
       "...............\n" +
       "...............\n" + 
       "...............\n" + 
       "...............\n" + 
       "...............\n" + 
       "...............\n" + 
       "...............\n" + 
       "..........VVV..\n" + 
       "..........VVV..\n" , spaceinvaders.recupererEspaceJeuDansChaineASCII());
   }


```

Implémentez ce test dans la classe de `SpaceInvadersTest`.
Une erreur de compilation apparaît puisque pour l'instant la méthode `positionnerUnNouveauVaisseau` est une méthode à deux paramètres uniquement.

Nous allons transformer la signature de cette méthode automatiquement à l'aide de l'IDE pour effectuer ce changement le plus rapidement possible et le plus surement possible.  
Sélectionnez `positionnerUnNouveauVaisseau` puis à l'aide d'un clic droit choisissez `Refactor -> Change Method Signature`.  
Vérifiez que vous voyez bien l'onglet `Parameters` et cliquez sur `Add` :  
- dans `Type`, saisissez `int`  
- dans `Name`, saisissez `vitesse` et  
- dans `Default Value`, saisissez `1`    
Peut-être avez-vous remarqué que la signature de la méthode se mettait à jour automatiquement dans le rubrique *Methode Signature Preview* au fur et à mesure que vous complétiez les différentes cases du tableau.

Cliquez sur `OK`.

**Consultez le fichier `SpaceInvadersTest`** et constatez que tous les appels à la méthode `positionnerUnNouveauVaisseau` à deux paramètres ont automatiquement été transformés en appels à la méthode `positionnerUnNouveauVaisseau` à 3 paramètres avec une valeur de `1` pour le dernier paramètre.

**Consultez le fichier `SpaceInvaders`** et constatez que la signature de la méthode `positionnerUnNouveauVaisseau` est désormais constituée de 3 paramètres d'entrée.   
Pour que cette méthode tienne compte la `vitesse`, il faut modifier son code et faire en sorte qu'il fasse désormais appel au constructeur à 3 paramètres. Pour cela, remplacez les deux instructions suivantes en fin de méthode :

```JAVA

    vaisseau = new Vaisseau(longueurVaisseau, hauteurVaisseau);
    vaisseau.positionner(x, y);
```

par l'instruction suivante : 

```JAVA

    vaisseau = new Vaisseau(dimension,position,vitesse);
```

Enregistrez et relancez vos tests !

Ils devraient normalement passer AU VERT car le test ajouté précédemment n'apporte en réalité aucun comportement nouveau.   
En effet, ce comportement était déjà testé par la méthode `test_VaisseauAvance_DeplacerVaisseauVersLaDroite` que vous pouvez supprimer pour ne conserver que la méthode de test que vous venons d'écrire (`test_VaisseauAvance_DeplacerVaisseauVersLaDroite_AvecVitesse`) et qui apporte le même comportement, mais de manière plus générique :smile:

Renommez d'ailleurs maintenant `test_VaisseauAvance_DeplacerVaisseauVersLaDroite_AvecVitesse` en `test_VaisseauAvance_DeplacerVaisseauVersLaDroite`.
 
> **Vous venez de faire des modifications dans votre code...**  
> ***N'oubliez pas de relancer les tests pour vérifier que le comportement de votre code n'a pas changé !***

Il est maintenant temps de s'interesser aux cas limites. Deux cas limites peuvent être envisagés :

* le premier concerne le cas où **le vaisseau doit rester immobile** car déjà en butée sur la droite de l'espace de jeu. 

* le second concerne le cas où **le vaisseau peut se déplacer partiellement** car il lui reste encore un peu de place avant d'atteindre la bordure droite de l'espace de jeu. Dans ce cas, le vaisseau peut se déplacer *un peu* jusqu'à la bordure droite, mais il faut bien veiller à ce que le vaisseau ne sorte pas de l'espace de jeu :smile:

#### 1.2 Cas *limite* : le vaisseau doit rester immobile car déjà en butée droite de l'espace de jeu

Ce premier cas correspond, dans le cas d'une vitesse égale à `1`, au cas de test suivant :

```JAVA

    @Test
    public void test_VaisseauImmobile_DeplacerVaisseauVersLaDroite() {

       spaceinvaders.positionnerUnNouveauVaisseau(new Dimension(3,2),new Position(12,9), 1);
       spaceinvaders.deplacerVaisseauVersLaDroite();
       assertEquals("" + 
       "...............\n" + 
       "...............\n" +
       "...............\n" + 
       "...............\n" + 
       "...............\n" + 
       "...............\n" + 
       "...............\n" + 
       "...............\n" + 
       "............VVV\n" + 
       "............VVV\n" , spaceinvaders.recupererEspaceJeuDansChaineASCII());
    }

```

Nous n'allons donc pas écrire de nouveau test, mais rendre le comportement de ce test plus générique en testant une vitesse de valeur **`3`** (à la place de **`1`**), ce qui revient à transformer le première instruction de la manière suivante :


```JAVA

    spaceinvaders.positionnerUnNouveauVaisseau(new Dimension(3,2),new Position(12,9), 3);

``` 

Enregistrez et relancez les tests !
Les tests devraient passer AU VERT !

#### 1.3 Cas *limite* : le vaisseau peut se déplacer partiellement et atteindre la butée

Ce cas concerne celui où **le vaisseau peut se déplacer partiellement** car il lui reste encore un peu de place avant d'atteindre la bordure droite de l'espace de jeu. Le déplacement est *partiel* car il correspond seulement à une partie des pixels utilisés dans un déplacement actuel car il faut bien sur faire en sorte que le vaisseau ne sorte pas de l'espace de jeu :smile:

Un tel cas de test n'était pas pris en compte lorsque la vitesse était fixée à `1`.  
Il faut donc écrire un nouveau test qui va apporter un nouveu comportement, celui du déplacement partiel et nous permettre ainsi de démarrer une nouvelle itération TDD.

##### 1.3.1 Etape RED : un test qui échoue

Le test suivant permet, par exemple, d'illustrer un déplacement partiel vers la droite.

```JAVA

    @Test
    public void test_VaisseauAvancePartiellement_DeplacerVaisseauVersLaDroite() {

       spaceinvaders.positionnerUnNouveauVaisseau(new Dimension(3,2),new Position(10,9),3);
       spaceinvaders.deplacerVaisseauVersLaDroite();
       assertEquals("" + 
       "...............\n" + 
       "...............\n" +
       "...............\n" + 
       "...............\n" + 
       "...............\n" + 
       "...............\n" + 
       "...............\n" + 
       "...............\n" + 
       "............VVV\n" + 
       "............VVV\n" , spaceinvaders.recupererEspaceJeuDansChaineASCII());
    }

```

Implémentez ce test dans votre fichier de tests et lancez les tests !

La barre est ROUGE : ce test échoue donc il apporte bien un nouveau comportement :smile:

##### 1.3.2 Etape GREEN : Faire passer le test

Pour faire passer le test, il faut intervenir dans la méthode `deplacerVaisseauVersLaDroite` de la classe `SpaceInvaders` afin de rectifier éventuellement le déplacement et repositionner le vaisseau sur la bordure droite de l'espace jeu, si celui-ci est sorti de l'espace jeu lors d'un déplacement autorisé, mais qui ne pouvait pas être *total* par manque de place.  
Au niveau du code, cela pourrait se traduire par quelque chose comme :


```JAVA

	public void deplacerVaisseauVersLaDroite() {
		if (vaisseau.abscisseLaPlusADroite() < (longueur - 1)) {
			vaisseau.seDeplacerVersLaDroite();
			if (!estDansEspaceJeu(vaisseau.abscisseLaPlusADroite(), vaisseau.ordonneeLaPlusHaute())) {
				vaisseau.positionner(longueur - vaisseau.longueur(), vaisseau.ordonneeLaPlusHaute());
			}
		}
	}

```

Relancez les tests !


##### 1.3.3 Etape Refactor
Nous ne ferons pas de refactoring pour le moment...

Il ne nous reste plus qu'à traiter de même le déplacement vers la gauche afin que ce dernier tienne également compte de la vitesse 


### 1. Déplacement vers la *gauche* pour une vitesse quelconque

#### 1.1 Cas *normal* (et un peu de refactoring au passage)

Nous allons directement modifier le test `test_VaisseauAvance_DeplacerVaisseauVersLaGauche` pour qu'il illustre un cas plus générique de déplacement vers la gauche.

Remplacez l'implémentation actuelle de votre méthode `test_VaisseauAvance_DeplacerVaisseauVersLaGauche` par cette implémentation :

```JAVA

    @Test
    public void test_VaisseauAvance_DeplacerVaisseauVersLaGauche() {

       spaceinvaders.positionnerUnNouveauVaisseau(new Dimension(3,2),new Position(7,9), 3);
       spaceinvaders.deplacerVaisseauVersLaGauche();

       assertEquals("" + 
       "...............\n" + 
       "...............\n" +
       "...............\n" + 
       "...............\n" + 
       "...............\n" + 
       "...............\n" + 
       "...............\n" + 
       "...............\n" + 
       "....VVV........\n" + 
       "....VVV........\n" , spaceinvaders.recupererEspaceJeuDansChaineASCII());
   }

```

Lancez-les tests et vérifiez qu'ils continuent à bien passer au VERT !

Comme précédemment deux cas limites vont être testés :

* le premier où **le vaisseau doit rester immobile** car déjà en butée sur la gauche de l'espace de jeu. 
* le second où **le vaisseau peut se déplacer partiellement** 

#### 1.2 Cas *limite* : le vaisseau doit rester immobile car déjà en butée gauche de l'espace de jeu

Placez-vous sur le test `test_VaisseauImmobile_DeplacerVaisseauVersLaGauche` et rendez son  comportement plus générique en testant cette fois-ci une vitesse de valeur **`3`**, ce qui revient à écrire le test suivant :

```JAVA

    @Test
    public void test_VaisseauImmobile_DeplacerVaisseauVersLaGauche() {

	   spaceinvaders.positionnerUnNouveauVaisseau(new Dimension(3,2),new Position(0,9), 3);
       spaceinvaders.deplacerVaisseauVersLaGauche();

       assertEquals("" + 
       "...............\n" + 
       "...............\n" +
       "...............\n" + 
       "...............\n" + 
       "...............\n" + 
       "...............\n" + 
       "...............\n" + 
       "...............\n" + 
       "VVV............\n" + 
       "VVV............\n" , spaceinvaders.recupererEspaceJeuDansChaineASCII());
     }

```

Enregistrez votre modification et relancez les tests !
Les tests devraient passer AU VERT !

#### 1.3 Cas *limite* : le vaisseau peut se déplacer partiellement et atteindre la butée

Comme précédemment, il est nécessaire d'écrire un nouveau test pour tester ce cas limite.

##### 1.3.1 Etape RED : un test qui échoue

Le test suivant permet, par exemple, d'illustrer un déplacement partiel vers la gauche.

```JAVA

    @Test
    public void test_VaisseauAvancePartiellement_DeplacerVaisseauVersLaGauche() {

       spaceinvaders.positionnerUnNouveauVaisseau(new Dimension(3,2),new Position(1,9), 3);
       spaceinvaders.deplacerVaisseauVersLaGauche();

       assertEquals("" + 
       "...............\n" + 
       "...............\n" +
       "...............\n" + 
       "...............\n" + 
       "...............\n" + 
       "...............\n" + 
       "...............\n" + 
       "...............\n" + 
       "VVV............\n" + 
       "VVV............\n" , spaceinvaders.recupererEspaceJeuDansChaineASCII());
     }

```

Implémentez ce test dans votre fichier de tests et lancez les tests !

La barre est ROUGE : ce test échoue donc il apporte bien un nouveau comportement :smile:

##### 1.3.2 Etape GREEN : Faire passer le test

Pour faire passer le test, il faut intervenir dans la méthode `deplacerVaisseauVersLaGauche` de la classe `SpaceInvaders` afin de rectifier éventuellement le déplacement et repositionner le vaisseau sur la bordure gauche de l'espace jeu, si celui-ci est sorti de l'espace jeu lors d'un déplacement autorisé, mais qui ne pouvait pas être *total* par manque de place.  
Au niveau du code, cela pourrait se traduire par quelque chose comme :


```JAVA

	public void deplacerVaisseauVersLaGauche() {
		if (0 < vaisseau.abscisseLaPlusAGauche())
			vaisseau.seDeplacerVersLaGauche();
		if (!estDansEspaceJeu(vaisseau.abscisseLaPlusAGauche(), vaisseau.ordonneeLaPlusHaute())) {
			vaisseau.positionner(0, vaisseau.ordonneeLaPlusHaute());
		}
	}

```

Relancez les tests !

##### 1.3.3 Etape Refactor
Nous ne ferons pas de refactoring pour le moment...


## Et bien, jouons maintenant !  <a id="testAcceptance"></a> 

Par contre maintenant, nous aimerions bien profiter de cette nouvelle fonctionnalité et faire avancer plus vite notre vaisseau dans l'application graphique, pour cela quelques interventions sont encore nécessaires :  
- d'une part faire en sorte que le moteur graphique fasse bien apparaître un vaisseau avec une vitesse donnée  
- d'autre part trouver la *bonne* valeur pour la vitesse de votre vaisseau, celle qui sera le mieux adaptée à votre application.

### 1. Faire en sorte que le moteur graphique fasse bien apparaître un vaisseau avec une vitesse donnée

Pour modifier la vitesse du vaisseau qui apparaît dans l'application graphique il faut modifier l'appel à la méthode `initialiserJeu` de la classe `SpaceInvaders` et faire en sorte que la méthode `positionnerUnNouveauVaisseau` prenne en paramètre la vitesse souahitée.
Pour faciliter le réglage de ce paramètre, nous utiliserons une nouvelle constante `VAISSEAU_VITESSE` dont la valeur sera arbitrairement fixée à `5` :

La méthode `initialiserJeu` de la classe `SpaceInvaders` devient :

```JAVA

	public void initialiserJeu() {
		Position positionVaisseau = new Position(this.longueur/2,this.hauteur-1);
		Dimension dimensionVaisseau = new Dimension(Constante.VAISSEAU_LONGUEUR, Constante.VAISSEAU_HAUTEUR);
		positionnerUnNouveauVaisseau(dimensionVaisseau, positionVaisseau, Constante.VAISSEAU_VITESSE);
	 }

```


Et la classe `Constante` :

```JAVA

    public class Constante {

	   public static final int ESPACEJEU_LONGUEUR = 150;
	   public static final int ESPACEJEU_HAUTEUR = 100;
	
	   public static final int VAISSEAU_LONGUEUR = 30;
	   public static final int VAISSEAU_HAUTEUR = 20;
	   public static final int VAISSEAU_VITESSE = 5;
	
	   public static final char MARQUE_FIN_LIGNE = '\n';
	   public static final char MARQUE_VIDE = '.';
	   public static final char MARQUE_VAISSEAU = 'V';
   }

```


### 2. Trouver la *bonne* valeur de vitesse pour le vaisseau

Il ne vous reste plus qu'à lancer le moteur graphique et à faire quelques essais de paramétrage pour trouver la *bonne* valeur de vitesse pour votre vaisseau !


## Committer les changements liés à cette nouvelle fonctionnalité <a id="commit"></a>

**Ce sprint est désormais terminé et la fonctionnalité *Choisir la vitesse du vaisseau* est semble-t-elle terminée et fonctionnelle : il est temps de committer les derniers changements dans votre gestionnaire de version !**  
Le commit pourrait refléter les changements apportés au travers du message suivant par exemple : **ajout vitesse du vaisseau**.

<!--Remarque : Si vous le souhaitez, vous pouvez tagger ce dernier commit `XX` avec un message de tag du genre `xxxxx`.-->

### Continuez par le [Sprint 4 : Tirer un missile depuis le vaisseau](SpaceInvaders_S4_TirerMissileDepuisVaisseau.md)