# Les blocs Évènements *(Events)*

Ces blocs constituent la base de vos scripts. Vous définirez vos comportements à l'intérieur de ces blocs.

Vous pouvez stocker des valeurs et accéder aux autres composants de l'objet de jeu grâce à la variable ``self``.

``self`` représente le composant Comportement Scripté de votre objet de jeu. Chaque comportement scripté de chaque objet de jeu est une instance différente, avec un cycle de vie propre, indépendant des autres comportements scriptés utilisant le même script que d'autres objets de jeu pourraient avoir.

----

## On | **Awake** | with instance as | **self**
![On Awake with instance as self](http://i.imgur.com/XanFz7k.png)

### Au **réveil** avec comme instance **soi-même**

À la création du script, ce bloc est appelé en tout premier.

Lorsque une scène est créée, tous les blocs ``On Awake with instance as self`` de tous les scripts sont exécutés chacun leur tour.
Si vous avez besoin d'initialiser un script, c'est ici que vous devriez le faire.

Attention toute fois, si un élément a besoin d'être initialisé avec le contenu d'un autre script, ce dernier risque de ne pas être encore initialisé. Préférez plutôt terminer l'initialisation dans le bloc ``On Start with instance as self``.

----

## On | **Start** | with instance as | **self**
![On Start with instance as self](http://i.imgur.com/XnLrq1M.png)

### Au **lancement** avec comme instance **soi-même**

À la création d'un comportement scripté, ce bloc est appelé après le bloc ``On Awake with instance as self``, et juste avant le premier ``On Update with instance as self``.

Lorsqu'une scène est créée, tous les blocs ``On Start with instance as self`` de tous les scripts sont exécutés après que tous les ``On Awake with instance as self`` des autres scripts aient étés effectués.

Utilisez ce bloc si vous avez besoin d'initialiser un comportement scripté après certaines autres initialisations ayant eu lieu dans un bloc ``On Awake with instance as self``.

----

## On | **Update** | with instance as | **self**
![On Update with instance as self](http://i.imgur.com/Vi8EErR.png)

### Au **tour de boucle de jeu** avec comme instance **soi-même**

Ce bloc est appelé à chaque tour de boucle de jeu, soit 60 fois par seconde.

C'est ici que vous devriez définir toute la logique répétitive du script.