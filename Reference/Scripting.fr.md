# Référence Scripting

Toutes les fonctions et constantes mises à disposition par CraftStudio pour vos scripts.

----
## Langage de script

Les scripts CraftStudio sont rédigés en [Lua](http://www.lua.org/about.html), un langage de programmation puissant, rapide et léger.

  * [Cours intensif de Lua](http://luatut.com/crash_course.html)  
  * [Apprendre Lua en 15 minutes](http://learnxinyminutes.com/docs/lua/) — pour les développeurs qui ont juste besoin d'un aperçu rapide du langage et de sa syntaxe.
  * [Apprendre Lua rapidement en français](http://www.luteus.biz/Download/LoriotPro_Doc/LUA/LUA_Training_FR/Introduction_Programmation.html) — pour les développeurs qui ont besoin d'apprendre rapidement le langage en français.
  * [Cours complet en français](http://wxlua.developpez.com/tutoriels/lua/general/cours-complet/) — pour comprendre les enjeux du scripting et les capacités de Lua.

----
## Version de l'API de script

Occasionellement, de nouvelles versions de CraftStudio peuvent empêcher certains scripts de fonctionner sur les anciens projets. Si une telle chose vient à arriver, les changements sont documentés dans la page des [Versions d'API](Scripting/API_Versioning.md).

----
## Fonctions globales et constantes de CraftStudio

[CraftStudio](Scripting/CraftStudio.md), [Input](Scripting/CraftStudio.Input.md), [Storage](Scripting/CraftStudio.Storage.md), [Screen](Scripting/CraftStudio.Screen.md), [Audio](Scripting/CraftStudio.Audio.md), [Physics](Scripting/CraftStudio.Physics.md), [Network](Scripting/CraftStudio.Network.md), [Web](Scripting/CraftStudio.Web.md)

----
## Manipuler les objets de jeu (*game objects*)

  * [GameObject](Scripting/GameObject.md) lui-même
  * Composants :
    * [Transform](Scripting/Transform.md) — Position, orientation & échelle
    * [Camera](Scripting/Camera.md) — Caméra
    * [ModelRenderer](Scripting/ModelRenderer.md), [MapRenderer](Scripting/MapRenderer.md), [TextRenderer](Scripting/TextRenderer.md) — Rendu de modèle, de map et de texte
    * [ScriptedBehavior](Scripting/ScriptedBehavior.md) — Comportement scripté
    * [Physics](Scripting/Physics.md) — Physique
    * [NetworkSync](Scripting/NetworkSync.md) — Réseau

----
## Ressources

[Map](Scripting/Map.md), [TileSet](Scripting/TileSet.md), [Sound](Scripting/Sound.md)

----
## Math

[Vector3](Scripting/Math/Vector3.md), [Quaternion](Scripting/Math/Quaternion.md), [Ray](Scripting/Math/Ray.md), [Plane](Scripting/Math/Plane.md) et [diverses fonctions mathématiques](Scripting/Math/Misc.md)