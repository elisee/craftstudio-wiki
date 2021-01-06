# Vue d'ensemble du moteur

----
## Boucle de jeu

La boucle de jeu est une suite d'évènements qui se répète constamment pendant que votre jeu s'exécute.

Quelques choses à savoir :

* Actuellement, la boucle de jeu parcourt l'arborescence d'objets de jeu en profondeur et met à jour chaque composant de chaque objet dans l'ordre où ils ont été créés. Ca serait peut-être mieux de mettre à jour tous les composants et les scripts du même type ensemble, aussi bien pour les performances (meilleure utilisation du cache) que pour une exécution plus naturelle.

* La fonction ```Behavior:Update()``` est appelée 60 fois par seconde. Si le jeu rame, la boucle de jeu essaie de rattraper son retard en sautant le rendu et en enchaînant plusieurs passes d'```Update``` à la suite. Dans le futur, ça aurait peut-être du sens d'ajouter une fonction ```Behavior:LazyUpdate()``` appelé aussi souvent que possible avec comme argument le temps qui s'est écoulé.

----
## Chargement des ressources (assets)

Actuellement, l'ensemble des ressources d'un jeu sont chargées en mémoire quand le jeu est lancé. Ca aurait sans doute du sens de permettre de charger certaines (voir la plupart) des ressources à la volée.