# Projekt und Asset Datenformat

Alle daten wurden gespeichert mit dem C# BinaryWriter mit ein paar erweiterungen für Vektoren and Quaternatoren.

Besuche https://gist.github.com/elisee/5580599 für ein CoffeeScript BinaryReader der die Datenformaten öffnen kann.

 * [Project](File_Formats/Project) — Gespeichert in ```Project.dat```, enthält metadaten, Spielsteuerungen und den Asset-Baum
 * [Models](File_Formats/Models), [Model Animations](File_formats/Model_Animations), [Maps](File_Formats/Maps), [Scripts](File_Formats/Scripts)
 * [Saved data](File_Formats/Saved_data) — Daten gespeichert mit der [CS.Storage API](Scripting/CraftStudio.Storage)