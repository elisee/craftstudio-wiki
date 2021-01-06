# L'API de CraftStudio

----
## CS, raccourci de CraftStudio

Plutôt que d'écrire ```CraftStudio.QuelqueChose``` à chaque fois, vous pouvez simplement utiliser ```CS.QuelqueChose```, qui économise du temps de frappe!

----
## CraftStudio.FindAsset
```lua
-- Retourne une table
CraftStudio.FindAsset( --[[ chemin vers la ressource ]], --[[ type de ressource (facultatif) ]] )
```

Retourne la ressource demandée (une texture, un modèle, une animation de modèle, une map, un set de blocs, un script ou un document).

Le chemin vers la ressource doit ressembler à ceci: **Personnages/Ennemis/Gobelin**. C'est le chemin de la ressource depuis la racine de la hiérarchie, chaque dossier étant séparé par une barre oblique (/).

Vous pouvez préciser le type de ressource en cas de besoin, pour résoudre l'ambiguïté entre plusieurs ressources ayant le même nom mais un type différent.

### Exemple: **Récupérer une animation pour la jouer**
```lua
local animMarche = CS.FindAsset( "Personnages/Marche", "ModelAnimation" )
self.gameObject.modelRenderer:SetAnimation( animMarche )
```

### **Liste des types de ressources** 
* Model
* Map
* ModelAnimation
* Script
* Scene
* Tile set


----
## CraftStudio.LoadScene
```lua
CraftStudio.LoadScene( --[[ ressource Scène à charger ]] )
```

Programme le chargement de la scène spécifiée à la fin de ce tour de la boucle de jeu (chaque tour dure 1/60ème de seconde).

Lorsque la nouvelle scène est chargée, tous les objets de jeu de la scène courante sont retirés.

Appeler cette fonction n'arrête pas immédiatement la fonction appelante. Il faudra éventuellement ajouter un retour de fonction (mot-clé ```return```) juste après si vous souhaitez quitter la fonction appelante.

Vous pouvez utiliser  ```CraftStudio.FindAsset``` pour obtenir une ressource de type Scène à passer à ```CraftStudio.LoadScene```.

----
## CraftStudio.AppendScene
```lua
-- Retourne un objet de jeu ou nil
CraftStudio.AppendScene( --[[ ressource de type scène à ajouter ]], --[[ objet de jeu auquel ratacher (facultatif) ]] )
```

Ajoute la scène demandée dans le jeu en créant tous les objets de jeu qu'elle contient. Contrairement à ```CraftStudio.LoadScene```, cette fonction ne supprime pas les objets de la scène en cours et n'attend pas le prochain tour de boucle du jeu : elle s'exécute immédiatement.

Vous pouvez accessoirement préciser un objet de jeu parent sur lequel tous les objets créés seront ajoutés.


Vous pouvez utiliser  ```CraftStudio.FindAsset``` pour obtenir une ressource de type Scène à envoyer à ```CraftStudio.AppendScene```. Si la scène demandée ne comporte qu'un seul objet de jeu racine, alors celui-ci est retourné, sinon la fonction renvoie ```nil```.

### Exemple: **Insérer une munition**

```lua
local munitionPrefab = CS.FindAsset( "Prefabs/munition", "Scene" )

-- En supposant que la scène contient un seul objet de jeu racine, il est retourné pour que l'on puisse s'en servir
local objetMunition = CS.AppendScene( munitionPrefab )

-- Placer la munition sur notre personnage avec un décalage quelconque
objetMunition.transform:SetPosition( self.gameObject.transform:GetPosition() + Vector3:New(1,0,1) )
```

----
## CraftStudio.Instantiate
```lua
CraftStudio.Instantiate( --[[ nom du nouvel objet de jeu ]], --[[ scène à instancier ]], --[[ objet de jeu auquel attacher (facultatif) ]] )
```

Créé un nouvel objet de jeu avec le nom spécifié, contenant une copie de la scène indiquée. Vous pouvez accessoirement préciser un objet de jeu parent sur lequel l'objet créé sera ajouté.

C'est très utile pour insérer un objet "préfabriqué" dans le jeu au lancement. Par exemple vous pouvez créer un personnage fait de multiples objets de jeu et de composants dans une scène différente et les insérer dans votre niveau grâce à ```CraftStudio.Instantiate```.

Si vous ne voulez pas un objet de jeu supplémentaire englobant votre scène instanciée, vous pouvez à la place utiliser ```CraftStudio.AppendScene```.

----
## CraftStudio.FindGameObject
```lua
-- Retourne un objet de jeu ou nil si l'objet n'existe pas
CraftStudio.FindGameObject( --[[ nom de l'objet de jeu ]] )
```

Retourne le premier objet de jeu avec le nom spécifié, ou ```nil``` si aucun n'a été trouvé.

----
## CraftStudio.CreateGameObject
```lua
-- Retourne l'objet de jeu créé
CraftStudio.CreateGameObject( --[[ nom ]], --[[ objet de jeu auquel ratacher (factultatif) ]] )
```

Créé un nouvel objet de jeu avec le nom spécifié et le retourne. Vous pouvez accessoirement préciser un objet de jeu parent sur lequel le nouvel objet créé sera ajouté.

Une fois votre objet de jeu créé, vous pouvez lui ajouter des composants avec ```GameObject:CreateComponent``` et ```GameObject:CreateScriptedBehavior```.

----
## CraftStudio.GetRootGameObjects
```lua
-- Retourne une liste des objets de jeu racine
CraftStudio.GetRootGameObjects()
```

Retourne une liste de tous les objets racines (non parentés) de votre jeu. Combiné avec ```GameObject:GetChildren()```, vous pouvez parcourir récursivement tous les objets de jeu de la scène courante.

### Exemple: **Afficher le nom et le nombre d'enfants directs de tous les objets racines**

```lua
for i, objetRacine in ipairs( CS.GetRootGameObjects() ) do
    print( objetRacine:GetName() .. " possède " .. #objetRacine:GetChildren() .. " enfants" )
end
```

----
## CraftStudio.Destroy
```lua
CraftStudio.Destroy( --[[ objet de jeu, composant ou ressource allouée dynamiquement ]] )
```
En fonction du type d'objet passé, la fonction :

  * détruit l'objet de jeu spécifié (et tous ses déscendants), ou
  * retire le composants spécifié de son objet de jeu, ou
  * libère une ressource allouée dynamiquement (voir ```Map.LoadFromPackage```)

----
## CraftStudio.Exit
```lua
CraftStudio.Exit()
```

Quitte le jeu à la fin du tour de boucle de jeu courant.