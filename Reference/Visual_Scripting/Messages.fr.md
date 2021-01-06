# Les blocs message *(Messages)*

----

## On | **Message** | *name* | with instance as | **self** | and data as | **data**
![On Message name with instance as self and data as data](https://lh5.googleusercontent.com/rlfp05OeeDw4Wcqg6yUHulbX0PLbkgjIQsfIUJBjC-SQ2GqkvBXRDiO2vqJP06CGmg=w1237-h529)

### Au **message** nommé ``nom`` avec comme instance **soi-même** et les donnés en tant que **data**
* ``name`` — le nom de votre message *(sans espaces, ne commence pas par un chiffre)*

Avec ce bloc, vous pouvez créer vos propres messages et communiquer entre différents scripts.
Vous pouvez aussi récupérer des données à travers la variable ``data`` et vous en servir dans le bloc.

----

## Send message | *name* | to | *game object* | with data | *value*
![Send message name to game object with data value](https://lh4.googleusercontent.com/C5gJW833v6yqDhMBQ9TX6FEyjZbDb7Ba4MjgC9csyyaApNX1d4LZmf8ThqRhcHGuZw=w1237-h529)

### Envoyer le message ``nom`` à l'``objet de jeu`` avec les données ``valeur``

 * ``name`` — le nom du message à appeler

 * ``game object`` — un bloc objet de jeu sur lequel envoyer le message

 * ``value`` — n'importe quel bloc de données à envoyer

Envoyez des messages et des données à d'autres scripts avec ce bloc.

L'objet de jeu qui recevra le message exécutera tous les blocs ``On Message name with instance as self and data as data`` portant le nom ``name`` de tous les scripts rattachés à lui.

Vous pouvez insérer n'importe quel type de donnée dans le paramètre ``value``. Si vous ne désirez pas passer de valeur, utilisez un bloc ``nothing``.