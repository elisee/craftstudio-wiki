# Misc Math Functions

----
## math.floor, math.ceil, math.round

```lua
-- Returns Number
math.floor( --[[ value (Number) ]] )

-- Returns Number
math.ceil( --[[ value (Number) ]] )

-- Returns Number
math.round( --[[ value (Number) ]] )
```

Returns the specified number respectively rounded down, rounded up or rounded to the nearest integer.

----
##math.clamp

```lua
-- Returns Number
math.clamp( --[[ value (Number) ]], --[[ min (Number) ]], --[[ max (Number) ]] )
```

Make sure that ```value``` is between ```min``` and ```max```. If ```value``` is inferior than ```min``` or superior than ```max```, it is brought back to the closest boundary.

----
## math.randomrange
```lua
-- Returns number
math.randomrange( --[[ lower (Number) ]], --[[ upper (Number) ]])
```

Generates a random real number (a float) between ```lower``` and ```upper```.

```lua
math.randomseed( os.time() )
```