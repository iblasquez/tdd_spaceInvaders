# Space Invaders en TDD

**L'objectif** de ce mini-projet est de développer un jeu de **space invaders** en **TDD**.

Dans ce README, vous trouverez les rubriques suivantes :

- [A propos du jeu *Space Invaders*](#aProposSpaceInvaders)   
- [A propos du TDD (*T*est *D*riven *D*evelopment)](#aProposTDD)
- [Organisation du mini-projet (accès aux différents sprints)](#organisation)
- [Références](#references) 
- [Commentaires, remarques et suggestions](#commentaires)  
- [Licence](#licence)

## A propos du jeu *Space Invaders* <a id="aProposSpaceInvaders"></a>

Space Invader est un **jeu de tir spatial** (*shoot'em up*).

Le système du jeu est le suivant (Extrait Wikipédia):

> [Space Invaders est un jeu fixe en deux dimensions.    
> Le joueur contrôle un canon laser qu'il peut déplacer horizontalement, au bas de l'écran.    
> Dans les airs, des rangées d'aliens se déplacent latéralement tout en se rapprochant progressivement du sol et en lançant des missiles.    
> L'objectif est de détruire avec le canon laser une vague ennemie, qui se compose de cinq rangées de onze aliens chacune, avant qu'elle n'atteigne le bas de l'écran.    
> Le joueur gagne des points à chaque fois qu'il détruit un envahisseur.   
> Le jeu n'autorise qu'un tir à la fois et permet d'annuler ceux des ennemis en tirant dessus.    
> La vitesse et la musique s'accélèrent au fur et à mesure que le nombre d'aliens diminue.     
> L'élimination totale de ces derniers amène une nouvelle vague ennemie plus difficile, et ce indéfiniment.   
> Le jeu ne se termine que lorsque le joueur perd, ce qui en fait le premier jeu sans fin.
> Les aliens tentent de détruire le canon en tirant dessus pendant qu'ils s'approchent du bas de l'écran.
> S'ils l'atteignent ou arrivent jusqu'au sol, ils ont réussi leur invasion et le jeu est fini.  
> De temps en temps, un vaisseau spatial apparait tout en haut de l'écran et fait gagner des points bonus s'il est détruit. 
> Quatre bâtiments destructibles permettent au joueur de se protéger des tirs ennemis.   
> Ces défenses se désintègrent progressivement sous l'effet des projectiles adverses et de ceux du joueur.   
> Le nombre de bâtiments n'est pas le même d'une version à l'autre.](https://fr.wikipedia.org/wiki/Space_Invaders)




*Remarques* :   

  
- Le site [http://www.classicgaming.cc/classics/space-invaders](http://www.classicgaming.cc/classics/space-invaders) est dédié à **Space Invaders**, on y trouve : [un descriptif détaillé du jeu](http://www.classicgaming.cc/classics/space-invaders/play-guide), des ressources graphiques, des ressources de son, ...
- Une définition de **jeu de tir spatial** peut être consulté dans le *Vocabulaire du jeu vidéo de Yolande Perron*  disponible [ici](https://www.oqlf.gouv.qc.ca/ressources/bibliotheque/dictionnaires/20120701_jeu_video.pdf).  


| <img src="https://upload.wikimedia.org/wikipedia/commons/8/80/Space_Invaders_style.png" alt="Space Invaders" width="400">
<img src="http://www.classicgaming.cc/classics/space-invaders/images/space-invaders-screenshot-points-sm.jpg" alt="Space Invaders sur Classic Game" width="400">  |  
Sources : images extraites de [Wikipédia](https://fr.wikipedia.org/wiki/Space_Invaders) et de [ClassicGaming](http://www.classicgaming.cc/classics/space-invaders/play-guide)



## A propos du TDD (*T*est *D*riven *D*evelopment) <a id="aProposTDD"></a>

Le ***développement dirigé par les tests*** (**T**est **D**riven **D**evelopment ou **TDD**) est une approche itérative et incrémentale de codage piloté par les tests unitaires. Un cycle de développement TDD se compose de trois étapes : 


<img src="http://iblasquez.github.io/presentation_TDD_CodingDojo/TDD_Mantra.png" alt="Mantra" width="400">



- La première étape (**RED**) consiste à écrire un nouveau test unitaire et vérifier qu'il échoue : ce test apporte ainsi un nouveau comportement.

- La deuxième étape (**GREEN**) consiste à écrire **au plus vite** un code de production pour faire passer le test précédent ainsi que les tests antérieurs. 

- La troisième étape (**REFACTOR**) est une phase de [refactoring](https://refactoring.com/) qui vise à faire émerger une [conception simple](http://referentiel.institut-agile.fr/yagni.html) afin d'améliorer la qualité de code.   
[4 critères de simplicité](http://referentiel.institut-agile.fr/simplicite.html)  ont été énoncés par Kent Beck (dans le cadre d'eXtreme Programming) :  
  - le code est doté de tests unitaires et fonctionnels et tous ces tests passent
  - le code ne fait apparaître aucune duplication
  - le code fait apparaître séparément chaque responsabilité distincte
  - le code contient le nombre minimum d'élément (classes, méthodes, lignes) compatible avec les trois premiers critères  
 Gardez à l'esprit ces critères lorsque vous êtes dans une phase de refactoring.

Remarque : Une présentation rapide du TDD est disponible [ici](http://iblasquez.github.io/presentation_TDD_CodingDojo)


## Organisation du mini-projet <a id="organisation"></a>

Ce mini-projet est découpé en plusieurs **sprints** regroupés en plusieurs objectifs :


**Objectif n° 1 :  
Un Space Invaders *minimum*  : un vaisseau, un missile, un envahisseur (MVP)**

- Sprint 0 : 
	- [Installation du socle technique](enonces/SpaceInvaders_S0_SocleTechnique.md)
	- [Rapide Analyse du problème](enonces/SpaceInvaders_S0_QuickDesignSession.md) 
- [Sprint 1 : Déplacer le vaisseau dans l'espace de jeu](enonces/SpaceInvaders_S1_DeplacerVaisseau.md)
- [Sprint 2 : Dimensionner le vaisseau](enonces/SpaceInvaders_S2_DimensionnerVaisseau.md)
- [Spike : Prise en main et intégration d'un moteur graphique](enonces/SpaceInvaders_Spike_MoteurGraphique.md)
- [Sprint 3 : Choisir la vitesse du vaisseau](enonces/SpaceInvaders_S3_ChoisirVitesseVaisseau.md)
- [Sprint 4 : Tirer un missile depuis le vaisseau](enonces/SpaceInvaders_S4_TirerMissileDepuisVaisseau.md)
- [Sprint 5 : Ajouter un envahisseur dans le jeu](enonces/SpaceInvaders_S5_Envahisseur.md)
- [Sprint 6 : Détecter une collision entre deux sprites](enonces/SpaceInvaders_S6_DetecterCollision.md)
- [Sprint 7 : Terminer la partie](enonces/SpaceInvaders_S7_TerminerPartie.md)

**Objectif n° 2 :  
Vers un Space Invaders plus *classique* (Améliorations du MVP)**
  
- [Sprint 8 : Permettre au vaisseau de tirer plusieurs missiles](enonces/SpaceInvaders_S8_TirerPlusieursMissiles.md)   
- [Sprint 9 : Envoyer une *ligne* d'envahisseurs](enonces/SpaceInvaders_S9_EnvoyerLigneEnvahisseurs.md)  
- [Sprint 10 : Gérer un score](enonces/SpaceInvaders_S10_GererScore.md) 
- [Sprint 11 : Tirer un missile depuis un envahisseur de manière aléatoire](enonces/SpaceInvaders_S11_TirerMissileDepuisEnvahisseur.md)
- [Sprint 12 : Envoyer une *horde* d'envahisseurs](enonces/SpaceInvaders_S12_EnvoyerHordeEnvahisseurs.md)   

**Objectif n° 3 : 
Le Space Invaders de vos rêves : smile:**

- [Sprint 13 & co : Toute amélioration possible pour réaliser le Space Invader de vos rêves](SpaceInvaders_S13_SpaceInvadersDeReve.md)


Les quatre premiers sprints sont écrits sous la forme de tutoriel et sont *extrêmement* détaillés : vous serez guidés pas à pas afin de vous plonger dans la démarche TDD et apprendre peu à peu à prendre en main votre IDE :smile:

Au fil des sprints, vous aurez de plus en plus d'autonomie pour développer votre mini-projet qui devra bien sûr respecter au mieux les bonnes pratiques de qualité de code ...

Un sprint un peu particulier (une sorte de [*spike*](http://agiledictionary.com/209/spike/)) doit également être ajouté. Il concernera la [mise en place d'un moteur graphique au sein de notre jeu](enonces/SpaceInvaders_MoteurGraphique.md) et sera consacré à la prise en main d'un moteur graphique simplifié et à son intégration au jeu. Idéalement, ce *spike* devrait être réalisée après le sprint 2 lorsque le vaisseau a une dimension. En réalité jusqu'à la livraison, le moteur graphique n'est pas vraiment nécessaire pour le développement de notre application puisque le comportement du jeu est vérifié et validé par les tests !    


Remarque pour ce projet dans le cadre du module M2104 :
- le *sprint* sera considéré comme une boîte de temps dédié au développement d'un ensemble de fonctionnalités autour d'une thématique commune. Suivant la vitesse à laquelle vous avancerez, plusieurs *sprints* pourront éventuellement être réalisés pendant une séance de TP. Vous *tirerez* ainsi les fonctionnalités au fur et à mesure de vos besoins, chaque binôme avançant à son propre rythme.    
- la séance consacrée à la mise en place du moteur graphique sera réalisée après le sprint 2 : soyez patient, et continuez tranquillement les sprints en attendant de mettre en place ce rendu visuel ;-)  
- Pour le module M2104, l'objectif n°1 est demandé.


Have fun !



Nous commencerons donc ce mini-projet par l'installation du socle technique : c'est par [ici](enonces/SpaceInvaders_S0_SocleTechnique.md).


## Références <a id="references"></a>

Ce mini-projet est en relation avec les enseignements suivants :

- Cours : [Quid du Test dans un développement logiciel ?](https://github.com/iblasquez/enseignement-iut-m2104/blob/master/slides/7_Tests.pdf)  
- Cours : [Sensibilisation aux bonnes pratiques de la programmation (qualité logicielle)](https://github.com/iblasquez/enseignement-iut-m2104/blob/master/slides/8_QualiteLogicielle_CleanCode.pdf)
- Présentation : [Coding Dojo : une aide à la pratique du TDD](http://iblasquez.github.io/presentation_TDD_CodingDojo)
- Atelier TDDlego : [Sensibilisation aux bonnes pratiques techniques du Software Craftsmanship : Lego® à la rescousse !](https://github.com/iblasquez/atelier-bonnes-pratiques-tdd-lego)
- Et plus généralement [tous les enseignements du module de conception (M2104)](https://github.com/iblasquez/enseignement-iut-m2104-conception) 

<!-- Tutoriel autour de [l'exemple *simplifié* du premier chapitre du livre Refactoring, Improving the Design of Existing Code de Martin Fowler](https://github.com/iblasquez/Refactoring_PremierExempleFowler) -->
<!-- Les références sont disponibles [ici](SpaceInvaders_References.md) -->


## Commentaires, remarques et suggestions <a id="commentaires"></a>
Pour les discussions, c'est par là : [https://github.com/iblasquez/tdd_spaceInvaders/issues](https://github.com/iblasquez/tdd_spaceInvaders/issues)  
Pour les propositions de contenu, de modification par ici : [https://github.com/iblasquez/tdd_spaceInvaders/pulls](https://github.com/iblasquez/tdd_spaceInvaders/pulls)

Et bien sûr, n'hésitez pas à personnaliser vos messages avec des [emojis](http://www.webpagefx.com/tools/emoji-cheat-sheet/) :smile:


## Licence <a id="licence"></a>
Tous les documents de ce dépôt sont placés sous licence CC BY-NC-SA :  [Creative Commons
Attribution - Pas d'Utilisation Commerciale - Partage dans les Mêmes Conditions](https://creativecommons.org/licenses/by-nc-sa/4.0/)

<img src="https://licensebuttons.net/l/by-nc-sa/3.0/88x31.png" width="100">

En savoir plus sur [les licences Creative Commons](https://creativecommons.org/licenses/?lang=fr-FR) ...

Toutefois, toute personne enseignant ou ayant enseignée au département Informatique de l'IUT du Limousin doit demander une autorisation préalable par écrit si elle souhaite utiliser les documents de ce dépôt. :smile: