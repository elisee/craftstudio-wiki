# L'API de CraftStudio.Input

----
## CraftStudio.Input.GetAxisValue
```lua
-- Retourne un nombre
CS.Input.GetAxisValue( --[[ nom de l'axe ]] )
```

Retourne la valeur numérique de l'axe demandé.

La valeur est comprise entre (-1, 1), sauf s'il s'agit d'un mouvement de souris, dans quel cas le delta en pixels de la souris depuis le dernier tour de boucle de jeu est retourné.

Les contrôles de jeu peuvent être définies dans l'onglet d'administration du projet.

----
## CraftStudio.Input.IsButtonDown
```lua
-- Retourne un booléen
CS.Input.IsButtonDown( --[[ nom du bouton ]] )
```

Retourne ``true`` si le bouton demandé est enfoncé, sinon la fonction renvoie ``false``.

Les contrôles de jeu peuvent être définies dans l'onglet d'administration du projet.

----
## CraftStudio.Input.WasButtonJustPressed, CraftStudio.Input.WasButtonJustReleased
```lua
-- Retourne un booléen
CS.Input.WasButtonJustPressed( --[[ nom du bouton ]] )
-- Retourne un booléen
CS.Input.WasButtonJustReleased( --[[ nom du bouton ]] )
```

Retourne ``true`` si le bouton demandé viens juste d'être appuyé (ou relâché) pendant le dernier tour de boucle de jeu (1/60ème de seconde), sinon la fonction renvoie ``false``

Les contrôles de jeu peuvent être définies dans l'onglet d'administration du projet.

----
## CraftStudio.Input.SetMouseVisible
```lua
CraftStudio.Input.SetMouseVisible( --[[ true ou false ]] )
```

Définit si le curseur devrait être visible ou non dans la fenêtre de jeu.

L'appel de cette fonction lorsque la souris est verrouillée est ignoré.

----
## CraftStudio.Input.LockMouse
```lua
CS.Input.LockMouse()
```

Masque le curseur de la souris et le verrouille à l'intérieur de la fenêtre de jeu. Utile dans les jeux qui utilisent la souris pour regarder aux alentours comme les jeux de tirs à la première personne.

----
## CraftStudio.Input.UnlockMouse
```lua
CS.Input.UnlockMouse()
```

Déverrouille la souris après avoir été verrouillée avec ``CraftStudio.Input.LockMouse``.

----
## CraftStudio.Input.GetMousePosition
```lua
-- Retourne une table
CS.Input.GetMousePosition()
```

Retourne une table avec les propriétés ``x`` et ``y`` contenant la position de la souris en pixels. ``x=0`` signifie que la souris est à gauche dans la fenêtre de jeu, ``y=0`` en haut.

Vous ne voudriez certainement pas utiliser cette fonction lorsque le curseur de la souris est verrouillé avec ``CraftStudio.Input.LockMouse`` puisque le curseur reste centré dans la fenêtre de jeu. Utilisez plutôt ``CraftStudio.Input.GetMouseDelta``.

----
## CraftStudio.Input.GetMouseDelta
```lua
-- Retourne une table
CS.Input.GetMouseDelta()
```

Retourne une table avec les propriétés ``x`` et ``y`` contenant le décalage de la souris en pixels depuis le dernier tour de boucle de jeu. Un ``.x`` positif signifie que le curseur s'est décalé vers la droite, un ``.y`` positif signifie vers le bas.

Cette fonction est particulièrement utile pour implémenter une vue à l'aide de la souris après l'avoir verrouillée avec ``CraftStudio.Input.LockMouse``.

### Exemple: **Mouvements basiques de vue à la première personne à la souris**

```lua
-- Script de la caméra
function Behavior:Awake()
    CS.Input.LockMouse()
    self.angleX = 0
    self.angleY = 0
end

function Behavior:Update()
    local deltaSouris = CS.Input.GetMouseDelta()
    
    -- Le delta horizontal correspond à une rotation autour de l'axe Y (gauche / droite)
    self.angleY = self.angleY - 0.2 * deltaSouris.x
    -- Le delta vertical correspond à une rotation autour de l'axe X (haut / bas)
    self.angleX = self.angleX - 0.2 * deltaSouris.y

    -- On empêche de regarder trop loin en hauteur
    self.angleX = math.clamp( self.angleX, -45, 45 )

    self.gameObject.transform:SetLocalEulerAngles( Vector3:New( self.angleX, self.angleY, 0 ) )
end
```

----
## CraftStudio.Input.OnTextEntered
```lua
CS.Input.OnTextEntered( --[[ fonction à appeler lorsque du texte est frappé ]] )
```

Définit la fonction qui va être appelée lorsque le joueur entre des caractères au clavier.

Lorsque vous ne voulez plus que votre fonction soit appelée, utilisez ``CS.Input.OnTextEntered( nil )`` pour réinitialiser le délégué.

Vous pouvez utiliser ``string.byte`` pour convertir le caractère en sa valeur numérique. C'est utile pour récupérer les caractères spéciaux comme le saut à la ligne (13), ou le retour arrière (8).

### Exemple: **Afficher chaque caractère entré par le joueur**

```lua
CS.Input.OnTextEntered( function( caractere )
  local numChar = string.byte(caractere)

  -- Les caractères de 0 à 31 sont des caractères de contrôle non affichables
  if numChar >= 32 then
      print( caractere )
  elseif numChar == 13 then
      print( "La touche Entrée vient d'être appuyée" )
  elseif numChar == 8 then
      print( "La touche retour arrière viens d'être appuyée" )
  end
end )
```