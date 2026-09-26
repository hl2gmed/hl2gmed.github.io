#  Getting Started — Global Variables<hr>

#  Global Tables
There are various global tables containing the active game  
state some of which are only available in specific scopes.

| Variable | Value | Scope |
|:--------:|:------|:------|
| `GM` | The loading gamemode | Available inside the gamemode's files <br/> Only available while the gamemode is loading
| `ENT` | The current scripted entity | Available inside the entity's files <br/><br/> `lua/entities/*.lua`
| `NPC` | The current scripted npc | Available inside the entity's files <br/><br/> `lua/npcs/*.lua`
| `SWEP` | The current scripted weapon | Available inside the weapon's files <br/><br/> `lua/weapons/*.lua`
| `_G` | All globals, including itself | Available anywhere 

#  NON CONSTANTS

##  CLIENT
This is true whenever the current script is executed on the client. ( client and menu states ) See States. Always present.

##  SERVER
This is true whenever the current script is executed on the server state. See States. Always present.
