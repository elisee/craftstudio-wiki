# Sound asset API

----
Sound assets let you play sound effects. You can create and upload sounds in your project and then play them back in scripting.

You can get a Sound asset by using [CraftStudio.FindAsset](CraftStudio.md)

There are two ways to play sounds: Either directly by using the Sound asset (which doesn't give you much control but is good for one-shot effects) or by creating a ```SoundInstance``` (which lets you pause / stop / resume / loop / set parameters while playing).

----
## Sound:Play

Plays the specified sound once. You can call it multiple times to play the same sound several times. The volume can be anything ```between 0.0 (mute) and 1.0 (full)```. You can also control the sound's pitch (both negative and positive numbers are accepted) and pan (left / right positioning).

For looping and stopping playing sounds, check out Sound:CreateInstance below.
```lua
Sound:Play( --[[ volume (Number) (Default 1) ]], --[[ pitch (Number) (Default 0) ]], --[[ pan (Number) (Default 0)]] )
```

### Example: **Playing a sound**
```lua
local sound = CS.FindAsset( "my sound" )

-- Plays the sound with default parameters (full volume)
sound:Play()
 
-- Plays the sound at half volume, with a higher pitch and panning to the right
sound:Play( 0.5, 0.8, 1 )
```

----
## Sound:CreateInstance

Creates an instance of the sound. Instances can be paused / resumed / stopped / looped and their parameters can be updated while playing.

```lua
-- Returns a SoundInstance
Sound:CreateInstance()
```

### Example: **Looping a sound**
```lua
local sound = CS.FindAsset( "my sound" )

-- Create an instance of the sound
local myInstance = sound:CreateInstance()

-- Set the instance to loop:
myInstance:SetLoop( true )
 
-- Play it
myInstance:Play()

-- ... Later on ...
-- Stop it
myInstance:Stop()
```

----
## SoundInstance:Play, SoundInstance:Stop

Plays or stop a instance of a sound
```lua
SoundInstance:Play()
SoundInstance:Stop()
```

----
## SoundInstance:Pause, SoundInstance:Resume

Pauses or resumes an instance of a sound
```lua
SoundInstance:Pause()
SoundInstance:Resume()
```

----
## SoundInstance:GetState

Returns the sound instance's current state.

Possible values are:

* ```SoundInstance.State.Playing```
* ```SoundInstance.State.Paused```
* ```SoundInstance.State.Stopped```

```lua
-- Returns the Soundstate
SoundInstance:GetState()
```

----
## SoundInstance:SetLoop, SoundInstance:GetLoop

Sets or gets whether the sound should loop or not.
```lua
SoundInstance:SetLoop( --[[ is looping (Boolean) ]] )

-- Returns loop state
SoundInstance:GetLoop()
```

----
## SoundInstance:SetVolume, SoundInstance:GetVolume

Sets or returns volume of sound instance, in the 0.0-1.0 range. With simple linear tweening, it may be used for fading music in/out.

```lua
SoundInstance:SetVolume( --[[ volume (Number) ]] )

-- Returns SoundInstance volume
SoundInstance:GetVolume()
```

### Example: **Fading in a sound**
```lua
function Behavior:Awake()
    local sound = CS.FindAsset( "some sound" )
    self.mySoundInstance = sound:CreateInstance()
    self.mySoundVolume = 0
    
    self.mySoundInstance:SetVolume( 0 )
    self.mySoundInstance:Play()
end
 
function Behavior:Update()
    if self.mySoundVolume < 1 then
        self.mySoundVolume = self.mySoundVolume + 0.05
        self.mySoundInstance:SetVolume( self.mySoundVolume )
    end
end
```

----
## SoundInstance:SetPitch, SoundInstance:GetPitch

Gets or sets the pitch adjustment, ranging from -1.0 (down one octave) to 1.0 (up one octave). 0.0 is normal pitch.

```lua
SoundInstance:SetPitch( --[[ pitch (Number) ]] )

-- Returns the SoundInstance pitch
SoundInstance:GetPitch()
```

----
## SoundInstance:SetPan, SoundInstance:GetPan

Panning, ranging from -1.0 (full left) to 1.0 (full right). 0.0 is centered.
```lua
SoundInstance:SetPan( --[[ pan (Number) ]] )

-- Returns the pan of a SoundInstance
SoundInstance:GetPan()
```