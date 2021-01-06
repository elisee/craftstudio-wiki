# L'API de CraftStudio.Storage

----

## Stockage persistant

Le stockage persistant vous permet de sauvegarder et charger des données entre plusieurs sessions de jeu, très utile pour enregistrer des paramètres de jeu ou sauvegarder la progression d'une partie.

Pour l'instant, ces données sont enregistrées directement sur votre ordinateur mais on peut imaginer qu'elles sont synchronisés avec un serveur sur Internet dans une future version.

----

## Identifiants

Les identifiants utilisés pour différencier les données sauvegardées et chargées doivent commencer par une lettre et contenir obligatoirement des caractères compris dans ``A-Z``, ``a-z``, ``0-9`` ou ``_``.

----

## CraftStudio.Storage.Save


```
#!lua

-- Sauvegarder des données
CraftStudio.Storage.Save( --[[ identifiant (chaine de caractères) ]], --[[ données (table) ou nil ]], --[[ fonction de rappel (fonction) ]] )
```
Sauvegarde la table passée en paramètre en données persistantes en utilisant l'identifiant précisé pour pouvoir les récupérer plus tard.  
Si le second paramètre utilisé est ``nil``, les données  persistantes associés à l'identifiant seront supprimés.

La sauvegarde des données peut prendre un peu de temps à cause de la latence du disque ou du réseau. Lorsque la sauvegarde a bien eu lieu (ou a échoué), la fonction passée en paramètre est appelée avec l'éventuelle erreur en tant que seul paramètre (ou ``nil`` si tout s'est bien déroulé).

S'il y a eu une erreur (disque dur plein, erreur de réseau ou tout autre raison), vous voudrez certainement avertir le joueur et lui proposer de réessayer.

### Exemple: **Sauvegarder le dernier niveau complété par le joueur**

```
#!lua

-- En considérant que nous avons cette table à enregistrer:
ProgressionJeu = {
    indexNiveau = 1
}

-- Le joueur viens juste de terminer le niveau, ajoutons un niveau à l'index
ProgressionJeu.indexNiveau = ProgressionJeu.indexNiveau + 1

-- Sauvegardons le pour plus tard!
CS.Storage.Save( "ProgressionDuJeu", ProgressionJeu, function(erreur)
    if erreur ~= nil then
        print( "Zut ! Nous n'avons pas pu sauvegarder votre progression." )
        return
    end

    print( "Progression sauvegardée avec succès !" )
end )
```
## CraftStudio.Storage.Load

----

```
#!lua
-- Charge les données depuis le stockage persistant
CraftStudio.Storage.Load( --[[ identifiant (chaine de caractères) ]], --[[ fonction de rappel (fonction) ]] )
```
Charge les données en utilisant l'identifiant spécifié depuis le stockage persistant.

Le chargement des données risque de prendre du temps à cause de la latence du disque ou du réseau. Lorsque le chargement a effectivement eu lieu (ou a échoué), la fonction passée en paramètre est appelée avec l'éventuelle erreur en tant que premier paramètre (ou ``nil`` si tout s'est bien déroulé), et les données chargées comme second paramètre (avec une valeur de ``nil`` si ces données n'existent pas).

S'il y a eu une erreur (erreur de disque dur, de réseau ou tout autre raison), vous voudrez certainement avertir le joueur et lui proposer de réessayer.

### Exemple: **Charger le dernier niveau complété par le joueur**

```
#!lua
-- Le joueur lance juste la partie, essayons de récupérer la progression
ProgressionJeu = {
    indexNiveau = 1
}

CS.Storage.Load( "ProgressionDuJeu", function(erreur, donnees)
    if erreur ~= nil then
        print( "Zut ! Nous n'avons pas pu charger votre progression." )
        return
    end

    if donnees ~= nil then
        ProgressionJeu = donnees
        print( "Chargement terminé avec succès !" )
        print( "Vous êtes au niveau" .. ProgressionJeu.indexNiveau )
    else
        -- C'est la première fois que le joueur lance une partie
        print( "Aucune donnée trouvée" )
    end
end )
```