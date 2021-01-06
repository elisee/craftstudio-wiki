# CraftStudio.Storage API

----
## Persistent storage

Persistent storage lets you save and load game data that will be kept between play sessions. It's great for storing settings or a player's progression throughout your game.

Currently, data will be saved locally on the player's computer but later versions of CraftStudio might provide support for cloud storage.

----
## Identifiers

Identifiers used to keep track of saved / loaded data should start with a letter and contain only the characters from the following ranges: A-Z, a-z, 0-9 or _.

----
## CraftStudio.Storage.Save
```lua
-- Saves data in persistent storage
CraftStudio.Storage.Save( --[[ identifier (string) ]], --[[ data (table) or nil ]], --[[ callback (function) ]] )
```

Saves the specified data table to persistent storage using the specified identifier for later retrieval. If the second parameter is ```nil``` instead, then any existing data associated with this identifier will be deleted.

Saving data might take some time because of disk or network latency. When the saving process is complete (or has failed), the function you passed will be called back with a potential error as its only parameter (with a value of ```nil``` if everything went right).

If there was an error (disk full, network failure or anything like that) then ideally you'd want to notify the player and allow them to retry.

### Example: **Saving the last level completed by a player**

```lua
-- Assuming we have a global table like this for instance:
GameProgress = {
    levelIndex = 1
}

-- The player just finished a level, let's increment levelIndex
GameProgress.levelIndex = GameProgress.levelIndex + 1

-- Write it down for later!
CS.Storage.Save( "GameProgress", GameProgress, function(error)
    if error ~= nil then
        print( "Oh no! There was an error saving your progress.")
        return
    end
    
    print( "Progress successfully saved!" )
end )
```

----
## CraftStudio.Storage.Load
```lua
-- Loads data from persistent storage
CraftStudio.Storage.Load( --[[ identifier (string) ]], --[[ callback (function) ]] )
```

Loads the data with the specified identifier from persistent storage.

Loading data might take some time because of disk or network latency. When the data has been loaded (or loading has failed), the function you passed will be called back with a potential error as its first parameter (with a value of ```nil``` if everything went right) and the loaded data table as its second parameter (with a value of ```nil``` if there was no data).

If there was an error (disk error, network failure or anything like that) then ideally you'd want to notify the player and allow them to retry.

### Example: **Loading the last level completed by a player**

```lua
-- The player just started the game, let's try to load their progress
GameProgress = {
    levelIndex = 1
}

CS.Storage.Load( "GameProgress", function(error, data)
    if error ~= nil then
        print( "Oh no! There was an error loading your progress.")
        return
    end
    
    if data ~= nil then
        GameProgress = data
        print( "Progress successfully loaded!" )
        print( "You're at level " .. GameProgress.levelIndex )
    else
        -- This is the first time the game is being played by this player
        print( "No saved data found" )
    end
end )
```
