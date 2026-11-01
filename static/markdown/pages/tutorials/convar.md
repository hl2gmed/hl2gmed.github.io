ConVars store information on the client and server that can be accessed using the developer console.
ConVar is short for "console variable". Sometimes it is also spelled like "CVar".<br/><br/>
There are two types of ConVars; client ConVars and server ConVars.

* [Global.CreateClientConVar](/static/pages/wip.html) is a clientside function used to create client ConVars. It is probably the most used. Only you, the client, can see the ConVars you make, unless 4th argument is set to true.

:You can see arguments and their descriptions on the function page.

* [Global.CreateConVar](/static/pages/wip.html) is a serverside function that creates a server ConVar. Clients won't be able to access this ConVar unless **FCVAR_REPLICATED** flag is set.

:You can see arguments and their descriptions on the function page.

##  Creating a Simple ConVar 

An example of a clientside ConVar would be:


```lua
 CreateClientConVar( "hello_enable", "1", true, false)
```


The above example would create a ConVar (only seen by you) called "hello_enable".
The ConVar, "hello_enable", starts off with a value of "1", and if you change it's value then it will be saved, even if you quit the game.
The ConVar does not send the value to the server whenever it's changed by you.

##  Getting ConVar value 

Once you have created your ConVar you can retrieve its value. You can do so by obtaining a ConVar object and using its methods to grab a value type:
* [Global.GetConVar](/static/pages/wip.html) - Retuns the <page>ConVar</page> object of the specified name
* [ConVar:GetInt](/static/pages/wip.html) - Retuns the integer value of the ConVar
* [ConVar:GetString](/static/pages/wip.html) - Retuns the string value of the ConVar
* [ConVar:GetBool](/static/pages/wip.html) - Retuns the boolean value of the ConVar
* [Player:GetInfo](/static/pages/wip.html) - Returns the player's convar in string
* [Player:GetInfoNum](/static/pages/wip.html) - Returns the player's convar in number
* etc.

For example:


```lua
local sbox_maxprops = GetConVar( "sbox_maxprops" )
print( sbox_maxprops:GetInt() )
```


Will print whatever the sbox_maxprops ConVar is set to.