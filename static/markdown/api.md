#  Lua Documentation<hr>

API of **Lua** Scripting language presented in *HL2GMed*.

## Globals
Type of objects that are defined in global Lua stack, and always accessable.
### Global Functions
Functions like `print`
```lua 
print()
```
or `Msg`
```lua
Msg()
```
are **global** functions.
You can call them any time, and in every script.

### Global Variables
Actually very simillar to *ENUMs*, and mostly used for same.
But unlike *ENUMs* global variables can contain any data or object.

Example of global variable
```lua
BASE_ENTITY = 'anim'
BASE_TYPES = {}
```
## Classes
Some systems that use OOP rules. Basically an entity but each with their own properties and methods.
```lua
entity:Remove()
```

## Libraries
Pre-built collection of various functions, that handle specific tasks. Pretty simillar to a table in global stack.
```lua
string.sub('Hello World', 1, 5)
``` 
or
```lua
table.sort({1,5,3})
```

## Hooks
Very powerful event system that lets your code run when something happens in the game.
```lua
hook.Add("PlayerSpawn", "MyHookName", function(ply)
    print('Player Spawned!')
end)
```

## Structs
Not a real Lua object, but just a information what properties objects can use.

Some variables that are defined in structs:
```lua
SWEP.PrintName = 'Weapon PrintName'
SWEP.Author = 'Author'
SWEP.Purpose = 'Shoot'
```

## ENUMs
Enumerations are the most common way to give friendly names to sets of numeric values.
Think of an ENUM as a label for a number that represents a specific option or state.
```lua
if ply:GetMoveType() == MOVETYPE_FLY then
    print("Player is flying!")
end
```

# Whole Lua API Documentation you can find [here](/static/documentation.html)