# Introduction
## What are Entities?
Nearly everything you can see and touch in Garry's Mod is an Entity. Any object with a position in the game world is an Entity. The Player is an Entity, props are Entities, even the the Game World itself is an Entity—albiet a special and unique one.

# Setup
## File Location
The file(s) that make up an Entity should be placed either in an Addon or in a Gamemode.
```lua
addons/
	├── my-addon-name/
    │	├── lua/
    │	│   ├── entities/
	│	│   │   └── ...
```

## File Structure
Entities can be created either using

* 3 separate files that each contain one Realm's code and configuration.
  * This approach helps with code organization.
  * The name of the folder containing these files (`my-entity-name` in the example below) will be used as the Entity's Class Name.
* The files are:
  * `cl_init.lua`
    * The Client Realm
  * `init.lua`
    * The Server Realm
  * `shared.lua`
    * The Shared Realm
```lua
entities/
   ├── my-entity-name/
   │   ├── cl_init.lua
   │   ├── init.lua
   │   └── shared.lua
```
# Creating an Entity
## Creating an Entity with separate files
shared.lua example:
```lua
-- Defines the Entity's type, base, printable name, and author for shared access (both server and client)
ENT.Type = "CPhysicsProp" -- Sets the Entity type to 'CPhysicsProp', indicating it's an scripted Entity.
ENT.Name = "Test Entity" -- The name that will appear in the spawn menu.
ENT.Spawnable = true -- Specifies whether this Entity can be spawned by players in the spawn menu.
```
init.lua example:
```lua
include("shared.lua")

-- Server-side initialization function for the Entity
function ENT:Initialize()
   self:SetModel( "models/custom_props/hl2gmed.mdl" ) -- Sets the model for the Entity.
   self:SetMoveType( 0 ) -- Sets how the Entity moves, using physics.
   self:SetSolid( 0 ) -- Makes the Entity solid, allowing for collisions.
end
```
cl_init.lua example:
```lua
include("shared.lua")

-- Client-side draw function for the Entity
function ENT:DrawModel()
end
```
