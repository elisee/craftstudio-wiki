# Glossaire

Définitions de différents mots rencontrés dans CraftStudio

----

## Serveur, projets et ressources

Un **serveur** CraftStudio est un logiciel que l'on peut exécuter sur un ordinateur pour héberger des projets. Quand vous démarrez CraftStudio, un serveur pour vos propres projets démarre automatiquement (à moins que vous ne l'ayiez désactiver dans les Options).

Quand vous souhaitez créer un nouveau jeu, il faut [créer un projet sur un serveur](../Tutorials/Introduction.md). Un **projet** possède, entre autres, un nom, description, type (jeu ou film), tableau blanc, des membres et des ressources.

Les **ressources** sont les modèles (personnages / objets faits à base de blocs), animations, maps, sets de bloc, scènes, scripts, sons ou polices de caractères.

----

## Scènes, objets de jeu et composants

Une **scène** est un type de ressource qui contient un arbre d'objets de jeu. Chaque **objet de jeu** est composé d'un ou plusieurs composants :

Le composant Transformation se trouve sur tous les objets de jeu et ne peut être supprimé. Il permet de les placer dans l'espace à travers une position, une orientation et une échelle.

Divers autres **composants** sont disponibles : Caméra (pour définir un point de vue depuis lequel votre jeu sera rendu), les Rendus de Modèle / Map / Texte, les Comportements Scriptés, les composants Physiques et les composants de Synchronisation Réseau.

----

## Variables globales, locales et propriétés

Une **variable** est un bocal (qui contient une valeur) avec une étiquette (le nom de la variable). Un nom de variable peut contenir n'importe quel lettre de l'alphabet ou chiffre mais ne peut pas contenir d'espace.

Une **variable globale** est une variable initialisée à la racine d'un script (c'est-à-dire hors de toute fonction ou bloc) sous la forme ```nomDeVariable = valeur```. Une telle variable est accessible et partagée entre tous les scripts.

Une **variable locale** est une variable initialisée sous la forme ```local nomDeVariable = valeur```. Sa durée de vie se limite à l'intérieur du bloc (fonction, condition, boucle, etc.) dans lequel elle est contenue et elle cesse d'exister dès que le bloc se termine. On peut définir une variable comme locale à la racine d'une script, auquel cas elle ne sera accessible que dans ce script.

Une **propriété** peut être ajouté à un objet de type ```table```:

```lua
maTable = {}
maTable.propriete = valeur
```

Dans les fonctions d'un comportement scripté dont le nom est préfixé par ```Behavior:```, le composant comportement scripté est accessible sous la variable ```self``` et il est possible de lui ajouter des propriétés. Comme chaque comportement scripté est unique, cela permet de créer des scripts réutilisables sur plusieurs objets.

Par exemple, on peut imaginer attacher une propriété ```self.vie``` à un comportement scripté utilisé sur tous les ennemis dans un jeu, et chaque ennemi aura donc une valeur de vie indépendante des autres ennemis.