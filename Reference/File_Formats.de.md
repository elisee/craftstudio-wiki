# Projekt und Asset Datenformat

Alle daten wurden gespeichert mit dem C# BinaryWriter mit ein paar erweiterungen für Vektoren and Quaternatoren.

Besuche https://gist.github.com/elisee/5580599 für ein CoffeeScript BinaryReader der die Datenformaten öffnen kann.

 * [Project](File_Formats/Project.md) — Gespeichert in ```Project.dat```, enthält metadaten, Spielsteuerungen und den Asset-Baum
 * [Models](File_Formats/Models.md), [Model Animations](File_formats/Model_Animation.mds), [Maps](File_Formats/Maps.md), [Scripts](File_Formats/Scripts.md)
 * [Saved data](File_Formats/Saved_data.md) — Daten gespeichert mit der [CS.Storage API](Scripting/CraftStudio.Storage.md)