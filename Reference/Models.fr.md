# Modèles

Les modèles dans CraftStudio sont des objets en 3D composés de blocs. Vous pouvez utiliser les modèles pour créer des personnages ou des objets pour votre jeu.

----
## Blocs

Chaque bloc qui compose un modèle a des caractéristiques: nom, position, orientation, taille, décalage pivot et étirement.

La taille définit le nombre de pixels qui composent le bloc pour chaque axe. Changer la taille du bloc change aussi le nombre de pixels utilisés dans la zone de dessin.

Le décalage pivot est utilisé pour définir l'origine du bloc. C'est utile pour les animation, notamment pour les articulations d'un personnage.

Voici un ensemble de blocs placés pour faire un modèle de personnage. Les blocs coloriés sont représentés dans la fenêtre en bas à gauche.

![Modeling.png](https://bitbucket.org/repo/ey9q4X/images/389906609-Modeling.png)

----
## Coloriage

Avant de commencer le coloriage, vous devez disposer les différents patrons sur la planche de manière à ce qu'il ne ce superposent pas (sauf si vous voulez que certains blocs ayaient la même texture). Vous pouvez agrandir la zone de dessin si nécessaire. Pour cela, cliquez sur le bloc voulu et déplacez son patron (qui c'est mis en surbrillance) dans la fenêtre en bas à gauche.

Un fois vos blocs placés, cliquez sur le bouton dessin afin de rentrer dans la zone de dessin et ainsi pouvoir dessiner et colorier vos blocs.

----
## Hiérarchie

Les blocs qui s'assemblent peuvent aussi être arrangés en hiérarchie. Cela signifie que un bloc peut être "parenté" à un autre qui sera "l'enfant". Les blocs enfants suivent leurs parents.

Ça marche comme la réalité. On peut dire que votre bras est "parent" de votre main qui est elle-même "parent" à vos cinqs doigts, par exemple.

![Hierarchies.png](https://bitbucket.org/repo/ey9q4X/images/1959504135-Hierarchies.png)

Les blocs peuvent avoir des enfants, qui peuvent eux-même en avoir et ainsi de suite, comme l'exemple du bras/main/doigts.