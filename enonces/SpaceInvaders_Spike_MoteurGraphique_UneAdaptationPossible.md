# Space Invaders - Une implémentation possible permettant de réaliser la partie du Spike sur *l'Adaptation du moteur graphique à notre Space Invaders*

**L'objectif** de ce document est de proposer une implémentation possible pour la partie *2.Adaptation du moteur graphique à notre Space Invaders* du [Spike destiné à la prise en main et intégration d'un moteur graphique](SpaceInvaders_Spike_MoteurGraphique.md)

Pour réaliser cet objectif, nous allons réaliser les trois étapes suivantes, à savoir :    
- [1. Implémentation de l'interface `Jeu` (dans `SpaceInvaders`)](#SpaceInvaders)    
- [2. Implémentation de l'interface `DessinJeu` (dans `DessinSpaceInvaders`)](#DessinSpaceInvaders)  
- [3. Implémentation de la classe de lancement du jeu Space Invaders (`Main`)](#Main)

## 1. Implémentation de l'interface `Jeu` (dans `SpaceInvaders`) <a id="SpaceInvaders"></a>

La classe `SpaceInvaders` n'est autre que la classe de `MonJeu` de l'exemple de code précédent, celle qui va *contrôler* le jeu (en connaître ses règles) et déclarer les *personnages* du jeu.
Pour mettre en place le moteur graphique, cette classe doit donc implémenter l'interface `Jeu` et redéfinir les méthodes `evoluer` et `etreFini` :  

* `etreFini` renverra `false` pour l'instant (le jeu ne sera jamais fini : la détection de fin de partie est une fonctionnalité qui sera réalisée ultérieurement)  
* `evoluer` sera implémentée de manière à faire évoluer les données du jeu en fonction de la commande utilisateur (comme indiqué dans la documentataion) selon nos besoins : actuellement, nous pouvons (et souhaitons) uniquement interagir avec le vaisseau et le déplacer de droite à gauche.

Une transformation possible de la classe `SpaceInvaders` pour l'intégration du moteur graphique est la suivante :


```JAVA

    public class SpaceInvaders implements Jeu {

	    //...

       @Override
       public void evoluer(Commande commandeUser) {
		
          if (commandeUser.gauche) {
              deplacerVaisseauVersLaGauche();
          }
		
         if (commandeUser.droite) {
	        deplacerVaisseauVersLaDroite();
         }

       }

   
      @Override
      public boolean etreFini() {
         return false; 
      }

    }

```

## 2. Implémentation de l'interface `DessinJeu` (dans `DessinSpaceInvaders`) <a id="DessinSpaceInvaders"></a>
Pour implémenter l'interface `DessinJeu`, il est nécessaire de créer une nouvelle classe (dans le package `fr.unilim.iut.spaceinvaders` de `src/main/java`), classe que vous appelerez **`DessinSpaceInvaders`**.

D'après la documentation (partie 1.1, 1.3 et annexes 3.2), cette classe a pour but de *dessiner l'image du jeu*. Elle doit implémenter l'interface `Jeu` et donc redéfinir la méthode `void dessiner(BufferedImage image)` qui a pour objectif de dessiner l'image du jeu sur l'image passée en paramètre.  
Dans l'état actuel de votre Space Invaders, la méthode `void dessiner(BufferedImage image)` n'aura qu'un seul objectif : celui de dessiner un vaisseau rectangulaire (à partir de la méthode `fillRect` comme dans l'exemple de code) de couleur grise par exemple.

***Remarques concernant l'affichage :***  
-> L'affichage se fera directement en pixel, nous n'utiliserons pas de constante **`TAILLE_CASE`** :smile:  
-> une méthode `dessinerdessinerObjet` comme dans l'exemple est-elle vraiment nécessaire ?   
-> **ATTENTION !!! L'origine du rectangle dessiné par `fillRect` et l'origine du `Vaisseau` sont différents !!!**   
En effet, la javadoc de la classe Graphics disponible [ici](https://docs.oracle.com/javase/7/docs/api/java/awt/Graphics.html) indique à propos de la méthode `fillRect` :  
`public abstract void fillRect(int x,int y, int width, int height)`  
*Fills the specified rectangle. The left and right edges of the rectangle are at x and x + width - 1. The top and bottom edges are at y and y + height - 1. The resulting rectangle covers an area width pixels wide by height pixels tall. The rectangle is filled using the graphics context's current color.*  
Ainsi le `x` de la méthode `fillRect` repésente l'*abscisse la plus à gauche* et le `y` de la méthode `fillRect` repésente l'*ordonnée  la plus *basse** c-a-d les coordonnées du coin gauche **supérieur** du rectangle à dessiner si l'axe des abscisses est vers la gauche et l'axe des ordonnées vers le bas, alors que que les coordonnées `x` et `y` de la `Position` `origine` d'un objet de type `Vaisseau` correspond aux coordonnées du coin gauche **inférieur**.  
***Soyez malin et utilisez les méthodes déjà existantes dans la classe `Vaisseau` pour récupérer facilement les *bonnes* coordonnées :smile: !*** 
    

D'autre part, d'après la partie 1.3 de la documentation, *la classe `DessinJeu` connait le `Jeu` afin de l'afficher lorsque le moteur le demande* c-a-d que *votre classe* `DessinSpaceInvaders` doit connaître *votre* `jeu` de type `SpaceInvaders`. Un tel objet `jeu` doit donc être déclaré en tant qu'attribut et un constructeur à un paramètre doit être proposé pour pouvoir l'instancier.


A partir, de ces informations et en nous aidant de l'exemple, nous pouvons proposer une implémentation possible pour la classe `DessinSpaceInvaders` :


```JAVA

    public class DessinSpaceInvaders implements DessinJeu {

	   private SpaceInvaders jeu;

	   public DessinSpaceInvaders(SpaceInvaders spaceInvaders) {
		   this.jeu = spaceInvaders;
	   }

	   @Override
	   public void dessiner(BufferedImage im) {
		   if (this.jeu.aUnVaisseau()) {
			   Vaisseau vaisseau = this.jeu.recupererVaisseau();
			   this.dessinerUnVaisseau(vaisseau, im);
		   }
	   }

	   private void dessinerUnVaisseau(Vaisseau vaisseau, BufferedImage im) {
		   Graphics2D crayon = (Graphics2D) im.getGraphics();

		   crayon.setColor(Color.gray);
		   	crayon.fillRect(vaisseau.abscisseLaPlusAGauche(), vaisseau.ordonneeLaPlusBasse(), vaisseau.longueur(), vaisseau.hauteur());

	   }

    }

```

Remarques :

* Avant de dessiner l'objet de type `Vaisseau`, il nous a paru opportun de tester la présence d'un tel objet dans l'espace de jeu :smile:

* Les instructions permettant de dessiner un rectangle auraient pu être écrites à ce stade du développement directement dans la méthode `dessiner` puisque le seul objectif de cette méthode consiste pour le moment à dessiner un objet de type `Vaisseau`.  
Pour une meilleure lisibilité, nous avons choisi d'extraire ces instructions dans une méthode `dessinerUnVaisseau`.  
A ce stade du développement, il ne nous paraît pas intéressant d'écrire une méthode `dessinerObjet`, trop générique par rapport à nos besoins [principe YAGNI](https://fr.wikipedia.org/wiki/YAGNI) (**Y**ou **A**ren't **G**onna **I**t) ! Nous aviserons plus tard s'il y a lieu de faire apparaître une telle méthode et déciderons alors de sa signature en fonction du contexte.

**Implémentez la classe `DessinSpaceInvaders` dans votre projet à partir du code précédent.**

Des erreurs de compilation sont apparaissent ?...  
Pas de problème, pour faire compiler ce code, il vous suffit de :

* **Dans la classe `SpaceInvaders`** :

	* Passez la méthode **`aUnVaisseau`** à **`public`**
	
	* Ajoutez une méthode **`recupererVaisseau`** (un simple *getteur*) similaire à :

```JAVA

	public Vaisseau recupererVaisseau() {
		return this.vaisseau;
	}

```


* **Dans la classe `Vaisseau`** :

	* Passer la méthode **`ordonneeLaPlusHaute`** à **`public`**

	* Ajouter deux méthodes **`hauteur`** et **`dimension`**, sorte de *getteur* qui renvoie individuellement la valeur de chacune des deux dimensions :
	

```JAVA

	public int hauteur() {
		return this.dimension.hauteur();
	}

	public int longueur() {
		return this.dimension.longueur();
	}
			
```



Il ne reste plus qu'à constater visuellement le résultat en lançant le jeu au travers du moteur graphique, pour cela il est nécessaire de mettre en place une classe `Main` comme dans l'exemple de code.


## 3. Implémentation de la classe de lancement du jeu Space Invaders (`Main`) <a id="Main"></a>

Pour disposer d'une application graphique et pouvoir lancer le moteur graphique, il nous faut une méthode `main`. Commencez donc par créer une classe `Main` (dans le package `fr.unilim.iut.spaceinvaders` de `src/main/java`) dédiée au lancement du moteur et qui implémentera `main` :smile:   
Astuce : Ecrivez `main` suivi de `CTRL+ESPACE` pour obtenir via l'auto-complétion d'Eclipse directement la signature d'un `main` :smile: 

Pour comprendre comment implémenter la classe `SpaceInvadersMain` nous allons nous appuyez sur la classe `Main` de l'exemple et sur la documentation.

* D'après la documentation (cf. partie 1.2 Description du fonctionnement du moteur), la classe `Main` doit disposer d'un objet `jeu` de type `SpaceInvaders` et d'un objet `afficheur`de type `DessinSpaceInvaders`.   
Ces deux objets sont nécessaire pour créer le `MoteurGraphique`. 

* Dans notre projet SpaceInvaders, la création du jeu va en fait être réalisé en deux étapes : un simple appel au constructeur suivi d'un appel à **une nouvelle méthode `initialiserJeu`** qui permettra de construire le contexte propre à notre jeu (et qui n'aura pas d'impact sur les tests déjà écrits).
Cette méthode, à écrire dans la classe `SpaceInvaders`, pourrait par exemple dans une premier temps positionner un vaisseau au milieu en bas de votre écran : smile:  

* Une fois le jeu initialisé, le `moteur` peut être créé et une fois créé, le `moteur` peut lancer le jeu en passant en paramètre la taille de l'écran.
Nous avons choisi d'utiliser des constantes pour faciliter le paramétrage du jeu ...  


```JAVA

    public class Main {

	    public static void main(String[] args) throws InterruptedException {

		    SpaceInvaders jeu = new SpaceInvaders(Constante.ESPACEJEU_LONGUEUR, Constante.ESPACEJEU_HAUTEUR);
		    jeu.initialiserJeu();
		    DessinSpaceInvaders afficheur = new DessinSpaceInvaders(jeu);

		    MoteurGraphique moteur = new MoteurGraphique(jeu, afficheur);
		    moteur.lancerJeu(Constante.ESPACEJEU_LONGUEUR, Constante.ESPACEJEU_HAUTEUR);
	    }

    }
 
```


```JAVA

    public class SpaceInvaders implements Jeu {

	   //...

        public void initialiserJeu() {
		    Position positionVaisseau = new Position(this.longueur/2,this.hauteur-1);
		    Dimension dimensionVaisseau = new Dimension(Constante.VAISSEAU_LONGUEUR, Constante.VAISSEAU_HAUTEUR);
		    positionnerUnNouveauVaisseau(dimensionVaisseau, positionVaisseau);
	    }
    }
 

```


**Remarque :**  
La taille de l'écran, (définie lors de l'appel de la méthode `lancerJeu(int width, int height)`)  et la taille de l'espace de jeu (définie lors de l'appel du constructeur `SpaceInvaders(int longueur, int hauteur)`) doivent être les mêmes (puisque nous n'avons pas souhaité gardé la constante **`TAILLE_CASE`** dans la classe permettant le dessin).
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

Il ne vous reste donc plus qu'à lancer votre application et interagir avec votre vaisseau pour vérifier que les classes **`SpaceInvaders.java`**, **`DessinSpaceInvaders.java`**, **`Vaisseau.java`** , **`Main.java`** et **`Constante.java`** ont été implémentées correctement :smile: ...

***Au cas où***...   
L'intégration du moteur graphique à notre jeu de Space Invaders nous a amené à modifier les classes suivantes :  
  
* **`SpaceInvaders.java`** dont vous pouvez consulter une implémentation possible [ici](src/SpaceInvaders_Spike.java)
* **`DessinSpaceInvaders.java`** dont vous pouvez consulter une implémentation possible [ici](src/DessinSpaceInvaders_Spike.java)
* **`Vaisseau.java`** dont vous pouvez consulter une implémentation possible [ici](src/Vaisseau_Spike.java)
* **`Main.java`** dont vous pouvez consulter une implémentation possible [ici](src/Main_Spike.java)
* **`Contante.java`** dont vous pouvez consulter une implémentation possible [ici](src/Constante_Spike.java)


### Une fois l'intégration réussie, vous pouvez continuer le tutoriel dédié au [Spike : Prise en main et intégration d'un moteur graphique](SpaceInvaders_Spike_MoteurGraphique.md)
