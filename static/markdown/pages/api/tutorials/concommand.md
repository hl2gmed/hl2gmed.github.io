#  Tutorials — Console Commands<hr>

Console commands are easy to add and remove. This is actually one of the easiest things you can learn in Lua and yet it could mean a lot to your actual coding process and time you take up to code whatever you are coding.

##  What are console commands? 
Console commands can be called from the console of the server or client at any time and the function of the command will be executed. This allows the server owner or client to perform actions upon the server. For example, kicking a player.<br/>

Please don't confuse console commands with console variables

##  How do I add them? 
You can add console commands anywhere in your code by using the `concommand.Add` function, just make sure that it is outside of any functions or hooks, so that the command will be added as soon as Lua system initializes.<br/>

Here's an example console command:


```lua
concommand.Add( "commandname", function( ply, cmd, args, str )
   print( ply:Nick(), cmd )
   PrintTable( args )
end )
```


The first argument is the command name.
The second argument is a function which have 3 arguments:
* Player - can either be a player object or, if called from the server, a NULL entity.
* Command - the command entered.
* Arguments - a table of strings containing the arguments entered. This is what you enter after the command, separated by a space (" ")
* Full string - the whole text that was entered into the console.

##  How do I remove them? 
You can remove console commands using the `concommand.Remove` function as so:


```
concommand.Remove( "commandname" )
```


Note that only commands added by Lua can be removed.
