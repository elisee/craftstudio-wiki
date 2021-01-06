# Les blocs de Contrôle *(Controls)* #

Les blocs de contrôle peuvent influencer le déroulement de l'exécution de votre script. C'est le commencement de l'interaction.

Cela permet d'adapter vos scripts à différentes situations ou de répéter une tâche pour de multiples objets.

----

## If | *boolean* ##

![If boolean](http://i.imgur.com/nH8Bgh5.png)

### Si | *booléen* ###

 * ``boolean`` — Une variable servant de condition

Si ``boolean`` est vrai, alors le contenu du bloc est exécuté.

----

## Else ##

![Else](http://i.imgur.com/IXmFdU3.png)

### Sinon ###

Lorsque la précédente condition n'a pas été satisfaite, le contenu de ce bloc est alors exécuté. Dans le cas contraire, il est ignoré.

Ce bloc doit obligatoirement être directement précédé soit d'un bloc ``If``, soit d'un bloc ``Else if``.

----

## Else if | *boolean* ##

![Else if](http://i.imgur.com/nNE662y.png)

### Sinon si | *booléen* ###

 * ``boolean`` — Une variable servant de condition

Lorsque la précédente condition n'a pas été satisfaite, le contenu de ce bloc est alors exécuté, à condition que ``boolean`` soit vrai. Dans le cas contraire, il est ignoré.

Ce bloc doit obligatoirement être directement précédé soit d'un bloc ``If``, soit d'un autre bloc ``Else if``.

----

## While | *boolean* ##

![While boolean](http://i.imgur.com/IS30fVI.png)

### Tant que | *booléen* ##

Si ``boolean`` est vrai, alors le contenu du bloc est exécuté.

À la fin de son exécution, la condition est vérifiée à nouveau. Si elle est toujours vraie, alors le contenu est exécuté une nouvelle fois. Ce bloc bouclera indéfiniment tant que ``boolean`` est vrai.

----

## Loop with | *variable* | from | *1* | to | *10* ##

![Loop with variable from 1 to 10](http://i.imgur.com/TxySyMX.png)

### Boucler avec une | *variable* | allant de | *1* | jusqu'à | *10* ###

 * ``variable`` —  le nom de votre variable *(sans espaces, ne commence pas par un chiffre)*
 * ``1`` — un nombre ou un bloc contenant une variable
 * ``10`` — un nombre ou un bloc contenant une variable

Cette boucle permet d'exécuter un certain nombre de fois son contenu.

Vous pouvez utiliser ``variable`` à l'intérieur du bloc comme variable locale. Elle prendra successivement les valeurs de 1 à 10, par pas de 1.

Vous pouvez changer les valeurs ``1`` et ``10`` en saisissant une autre valeur ou en y insérant un bloc.

----

## Foreach | **key▼** | *variable* | value | *variable* | in | *table* ##

![Foreach key variable value variable in table](http://i.imgur.com/n5XTfRX.png)

### pour chaque | **clé▼** | *variable* | valeur | *variable* | dans la | *table* ###

**key▼** peut prendre les valeurs

 * **key** — clé de la table

 * **index** —  index dans la table

----

* ``variable`` —  le nom de votre variable qui contiendra la clé ou l'index

* ``variable`` —  le nom de votre variable qui contiendra la valeur à la clé ou l'index correspondant de la table

* ``table`` — La table sur laquelle vous voulez parcourir le contenu

``variable`` prendra successivement toutes les clés ou index contenus dans ``table`` et le deuxieme ``variable`` prendra successivement toutes les valeurs associés aux clés ou index de ``table``.

Cela permet d'effectuer des opérations sur tous les éléments d'une table sans avoir à en connaitre son contenu ou son nombre d'éléments.

----

## — | comment ##

![comment](http://i.imgur.com/SuONwHu.png)

### — | commentaire ###

``comment`` — un commentaire

Ce bloc n'effectue aucune opération.

Il sert simplement à écrire du texte dans votre script pour le rendre plus lisible, ou pour expiquer comment fonctionne une portion de bloc.

Son contenu est exécuté normalement.