# Setting up & managing a server

----
## Stand-alone server

CraftStudio comes with a built-in server which can be managed by clicking on the My Server button from within CraftStudio. But if you want to keep a server running at all time, it might be simpler to run it from the command line (on Linux for instance).

You'll need your Mono version to be at least 2.10 (older versions won't work).

To do install all the dependencies on an Ubuntu system, you'll need to run the following command:

```
sudo apt-get install mono-runtime libmono-system-windows-forms4.0-cil libmono-system-core4.0-cil libmono-system-numerics4.0-cil libmono-system-runtime-serialization4.0-cil libmono-system-xml-linq4.0-cil libmono-microsoft-csharp4.0-cil libsdl-mixer1.2
```

Then you can download the latest server binaries from the [CraftStudio builds page](http://craftstud.io/builds) and run the server with:

```
mono CraftStudioServer.exe /p=4232 /admins=username1,username2,...
```

----
## Server commands

This is a list of commands that might be useful in managing a server. Commands should be entered in a project's chat input box.

### Search
```
/search [search_string]
```
Type this in the project's home tab to look for assets containing the specified text in their name. The command returns all matches with some info about each. This is useful for locating assets that have been trashed and you want to restore.

### Restore
```
/restore [asset_id]
```
This will untrash the asset with the specified ID. The server will try to restore the asset to its parent folder, but if the folder has been deleted, it will it put the restored asset at the root instead.
(You can also restore assets directly from the administration tab instead of using commands)

### Open
```
/open [asset_id]
```
Similar to the previous two, this command needs to be typed in the project's home tab. It will open the asset with the given id if it exists and it hasn't been trashed.

### Get an asset's ID
```
/assetid
```
Type this command in an asset's tab to get its ID. You can then share it with other people and they can use it to join you with the /open command.

### Get a link to the current project
```
/projectlink
```
Prints a link you can share on the Web for people to join your project.

### Get the current project's GUID
```
/projectguid
```
Prints the project's globally unique identifier. Mostly useful for debugging.

### Delete a project
You can unload and disable a project, provided you have admin rights **on the server** (being an administrator of the project is not enough). To do so, type the following command:
```
/deleteproject
```
and add a space followed by "yes for real".
All members will be disconnected, the project will be unloaded and the project's folder will be renamed to "[Project GUID] (deleted)". It is up to you to delete the folder once and for all.

If you change you mind, stop the server, remove the " (deleted)" part of the folder name and restart the server.

### Empty a project's recycle bin
```
/emptyrecyclebin
```

When you trash an asset, it gets moved to the recycle bin (which you can find in the project's administration tab). Project administrators can use this comand to empty the recycle bin and remove all trashed assets at once from the project entirely.

### Purge a project's deleted asset files
```
/purgefiles
```

When assets are deleted, their entry is removed from the project's entry list, but the actual data files are left intact. Most asset files are very small so you shouldn't worry about that until you have a very huge project. In the very rare case where you need to reclaim disk space and have deleted a lot of assets, a project administrator can use this command to systematically delete all data files that aren't part of the project anymore.