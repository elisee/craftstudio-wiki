# Projekt und Asset Datenformat

Alle daten wurden gespeichert mit dem C# BinaryWriter mit ein paar erweiterungen für Vektoren and Quaternatoren.

Besuche https://gist.github.com/elisee/5580599 für ein CoffeeScript BinaryReader der die Datenformaten öffnen kann.

 * [Project](File_formats/Project.md) — Gespeichert in ```Project.dat```, enthält metadaten, Spielsteuerungen und den Asset-Baum
 * [Models](File_formats/Models.md), [Model Animations](File_formats/Model_Animation.mds), [Maps](File_formats/Maps.md), [Scripts](File_formats/Scripts.md)
 * [Saved data](File_formats/Saved_data.md) — Daten gespeichert mit der [CS.Storage API](Scripting/CraftStudio.Storage.md)
