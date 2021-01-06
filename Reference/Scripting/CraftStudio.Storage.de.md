# CraftStudio.Storage API

----
## Storage API,

Die Storage-API stellt dir die möglichkeit zur verfügung, einen Variable(Integer,String,Boolean und Tabellen)
dauerhaft zu speichern, sodass die daten beim nächsten Spielstart wieder zur verfügung stehen
----
## Identifizierungsnummern

Identifizierungsnummern werden benutzt um den daten einen Namen zu geben / geladene daten beginnen mit einem Buchstaben, und können nur folgende zeichen enthalten: A-Z, a-z, 0-9 oder _.

ANMERKUNG DES ÜBERSETZERS:
Zeichen wie Ü, Ö, Ä oder À werden nicht unterszützt

Code von Élisée
----
## CraftStudio.Storage.Save
```lua
-- Speichert daten dauerhaft
CraftStudio.Storage.Save( --[[ Identifizierungsnummer (string) ]], --[[ daten (table) oder nichts(nil) ]], --[[ rückgabe (function) ]] )
```

Speichert die Angegebenen daten im dauerhaften speicher. Wenn der Zweite Parameter [LEER] also ```nil``` ist wird die gespeicherten daten bzw. Identifizierungsnummern PERMANENT gelöscht

Da beim speichern auf der Festplatte (oder im Netzwerk) manchmal etwas länger dauern kann, gibt es eine möglichkeit auszulesen, ob das speichern geklappt,(oder auch nicht geklappt) hat, die funktion(Argument 3) wird mit dem Fehler als Argument gestartet (wenn es [LEER] also ```nil``` ist, hat alles geklappt).

Wenn ein fehler auftritt(Festplatte voll, Netzwerkfehler oder soetwas) dann sollte der spieler ja informiert werden, oder?

### Beispiel: **Der letzte fortschritt des Spielers speichern**

Code von Élisée
```lua
--Also, man nehme eine tabelle(so wie das hier):
GameProgress = {
    levelIndex = 1
}

-- und wenn der spieler ein Level geschafft hat, dan wird das in eine Variable gschrieben
GameProgress.levelIndex = GameProgress.levelIndex + 1

-- und dann wird es gespeichert, für später!
CS.Storage.Save( "GameProgress", GameProgress, function(error)
    if error ~= nil then
        print( "FEHLER >> Oh nein! Da ist ein fehler beim speichern aufgetreten! :(")
        return
    end
    
    print( "INFO >> Die daten wurden FEHLERFREI gespeichert!" )
end )
```

----
## CraftStudio.Storage.Load
```luDaten laden mit der Identifizierungsnummer

Das laden kann bekantlich ja einiges an Zeit kosten. Wenn die daten geladen wurden (oder wenn ein Fehler aufgetreten ist), wird die angegebene funktion ausgelöst mit dem ersten parameter als Fehler:
(Wert: ```nil``` hat alles geklappt) und die variable ist der Zweite Parameter
(Wert: ```nil``` wenn keine Daten vorhanden sind).
-- Lädt Daten aus dem Permanenten speicher
CraftStudio.Storage.Load( --[[ identifier (string) ]], --[[ callback (function) ]] )
```


Wenn ein Fehler aufgetreten ist(Festplatte voll, Netzwerkfehler oder soetwas), dann wollen wird das natürlich dem Spieler mitteilen
### Beispiel: **Laden des letzten Levels, das der Spieler gsepielt hat**

```lua
-- Der spieler hat das spiel gestartet, also versuchen wir die daten zu laden...
GameProgress = {
    levelIndex = 1
}

CS.Storage.Load( "GameProgress", function(error, data)
    if error ~= nil then
        print( "FEHLER >> Oh nein! Da ist ein fehler beim laden aufgetreten! :(")
        return
    end
    
    if data ~= nil then
        GameProgress = data
        print( "INFO >> Die daten wurden FEHLERFREI gespeichert!" )
        print( "INFO >> Du bist momentan in level " .. GameProgress.levelIndex )
    else
        -- Wenn der spieler das erste mal spielt
        print( "WARNUNG >> Keine daten vorhanden!" )
    end
end )
```


Übersetzt von Luca Gronmaier, am 12.09.2015 um 2.:50Uhr
aus dem Orginal Englischem:
http://learn.craftstud.io/Reference/Scripting/CraftStudio.Storage von Élisée@SparklinLabs