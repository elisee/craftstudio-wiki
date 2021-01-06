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

Occasionellement, de nouvelles versions de CraftStudio peuvent empêcher certains scripts de fonctionner sur les anciens projets. Si une telle chose vient à arriver, les changements sont documentés dans la page des [Versions d'API](Scripting/API_Versioning).

----
## Fonctions globales et constantes de CraftStudio

[CraftStudio](Scripting/CraftStudio), [Input](Scripting/CraftStudio.Input), [Storage](Scripting/CraftStudio.Storage), [Screen](Scripting/CraftStudio.Screen), [Audio](Scripting/CraftStudio.Audio), [Physics](Scripting/CraftStudio.Physics), [Network](Scripting/CraftStudio.Network), [Web](Scripting/CraftStudio.Web)

----
## Manipuler les objets de jeu (*game objects*)

  * [GameObject](Scripting/GameObject) lui-même
  * Composants :
    * [Transform](Scripting/Transform) — Position, orientation & échelle
    * [Camera](Scripting/Camera) — Caméra
    * [ModelRenderer](Scripting/ModelRenderer), [MapRenderer](Scripting/MapRenderer), [TextRenderer](Scripting/TextRenderer) — Rendu de modèle, de map et de texte
    * [ScriptedBehavior](Scripting/ScriptedBehavior) — Comportement scripté
    * [Physics](Scripting/Physics) — Physique
    * [NetworkSync](Scripting/NetworkSync) — Réseau

----
## Ressources

[Map](Scripting/Map), [TileSet](Scripting/TileSet), [Sound](Scripting/Sound)

----
## Math

[Vector3](Scripting/Math/Vector3), [Quaternion](Scripting/Math/Quaternion), [Ray](Scripting/Math/Ray), [Plane](Scripting/Math/Plane) et [diverses fonctions mathématiques](Scripting/Math/Misc)