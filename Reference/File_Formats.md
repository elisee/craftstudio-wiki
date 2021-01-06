# Project and asset file formats

All data is written using C#'s BinaryWriter with a few extensions for vectors and quaternions.

See https://gist.github.com/elisee/5580599 for a CoffeeScript BinaryReader that can read the various primitive data types.

 * [Project](File_Formats/Project.md) — Data saved in the ```Project.dat``` file, includes metadata, game controls and asset tree
 * [Models](File_Formats/Models.md), [Model Animations](File_formats/Model_Animations.md), [Maps](File_Formats/Maps.md), [Scripts](File_Formats/Scripts.md)
 * [Saved data](File_Formats/Saved_data.md) — Data saved with the [CS.Storage API](Scripting/CraftStudio.Storage.md)