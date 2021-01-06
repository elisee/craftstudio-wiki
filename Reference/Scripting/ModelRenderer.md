# ModelRenderer component API

----
## ModelRenderer:GetModel, ModelRenderer:SetModel
```lua
-- Returns a Model
ModelRenderer:GetModel()
ModelRenderer:SetModel( --[[ model asset to display ]], --[[ clear animation (optional default=true) ]] )
```

Gets or sets the displayed model. You can get a model to display with ```CraftStudio.FindAsset```.

### Example: **Set the model displayed by a model renderer**

```lua
local modelToDisplay = CS.FindAsset( "A model asset", "Model" )

local modelRndr = CS.FindGameObject( "An object with a model renderer" ).modelRenderer
modelRndr:SetModel( modelToDisplay )
```

----
## ModelRenderer:GetAnimation, ModelRenderer:SetAnimation
```lua
-- Returns an Animation
ModelRenderer:GetAnimation()
ModelRenderer:SetAnimation( --[[ ModelAnimation asset ]] )
```

Gets or sets the current animation for this model. It will start playing right away unless you called ```ModelRenderer:StopAnimationPlayback```.

You can get animations to use with ```SetAnimation``` by calling ```CraftStudio.FindAsset```.

----
## ModelRenderer:GetAnimationDuration
```lua
-- Returns duration in seconds
ModelRenderer:GetAnimationDuration()
```

Gets the current animation's duration in seconds. You can multiply the returned number by 30 to get the number of frames.

----
## ModelRenderer:StartAnimationPlayback
```lua
ModelRenderer:StartAnimationPlayback( --[[ true or false (optional, defaults to true) ]] )
```

Starts animation playback (provided it was stopped earlier with ```ModelRenderer:StopAnimationPlayback```) or changes the way an animation plays back. Pass ```false``` to disable looping.

----
## ModelRenderer:StopAnimationPlayback
```lua
ModelRenderer:StopAnimationPlayback()
```

Stops animation playback.

----
## ModelRenderer:SetAnimationTime
```lua
-- Returns the current animation time in seconds
ModelRenderer:GetAnimationTime()
ModelRenderer:SetAnimationTime( --[[ time in seconds ]] )
```

Gets or sets the current animation time in seconds.

You could call ```ModelRenderer:StopAnimationPlayback``` and then use ``SetAnimationTime`` to move forward / backward in time in a script.

Model animations are stored at 30 frames per second. This means you can skip to the 3rd frame on an animation by using ```ModelRenderer:SetAnimationTime( 3 / 30 )``` for instance.

----
## ModelRenderer:IsAnimationPlaying
```lua
-- Returns a boolean
ModelRenderer:IsAnimationPlaying()
```

Returns ```true``` if an animation is currently playing.

----
## ModelRenderer:GetOpacity, ModelRenderer:SetOpacity
```lua
-- Returns a number
ModelRenderer:GetOpacity()
ModelRenderer:SetOpacity( --[[ opacity ]] )
```

Gets or sets the model renderer's opacity (between 0.0 and 1.0)

----
## ModelRenderer:GetBlockTransform
```lua
-- Returns a table
ModelRenderer:GetBlockTransform( --[[ block name ]] )
```

Returns a table with ```.position``` and ```.orientation``` keys containing the specified model block's current position and orientation.

This method is useful for making a weapon or tool follow an animated arm for instance.