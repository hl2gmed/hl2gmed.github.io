#  Getting Started — Creating & Running<hr>

#  Introduction

A Lua file is called a script. Lua scripts are plain text files. To create and edit Lua scripts, you need a plain text editor such as notepad.

You can use any plain text editor, but **you are going to have a hard time** if you aren't using one of the many available [Lua Editors](/static/pages/starters/le.html), such as QuickEdit Text Editor or ACode.

During these tutorials, we'll refer to your preferred text editor as "notepad".

<div class="warning"><b>⚠️WARNING:</b><br><i><b>Do not use Text Editor.</b>

It is a formatted text editor, not a plain text editor. It will put useless tags in around your code that will cause it to fail when loading. As a rule of thumb, if you can have text that uses two different fonts in one file, then it is not a plain text editor.</i></div>

#  Creating the script

For our first script, we're not going to do anything too complex. We'll learn how to print a message into the console.

The [print](/static/pages/wip.html) function does exactly that. Type the following code into your chosen editor :


```
print( "Hello World!" )
```


You're done! Wasn't that easy? It should have been.

## Explanation
`print` is a function. A function is a command that does something when you call it. Many functions can take arguments, which is data you give the function to change exactly what it does. In this case, `print()` takes only one argument, which is a string (a series of letters, numbers, spaces, and so on), and when `print()` is called, it puts that string into the console in Half-Life 2 Garry's Mod Edition.

# Saving the script

You're now ready to save the actual Lua file. To find your Lua folder, follow the following path - depending on where you have installed Half-Life 2 Garry's Mod Edition on your phone, this path may be different, but will look something like this:


```
/storage/emulated/0/srceng/hl2gmed/lua/
^^^^^^^^^^^^^^^^^^^^^^^^^^^
	This may be different!
```


In the filename box, type `helloworld.lua` (Note that you must specify `.lua`), and in the Save As type box, select All Files. Now, just press enter (or press the save button) to save your script.

# Running the script
To run any of your scripts, you need to be playing a map. Once in game, open the developer console and type the following:


```
lua_openscript helloworld.lua
```


Press enter. If you did everything correctly up to this point, you should see a message in the console:


```
Hello World!
```


Congratulations, you have written and run your first Lua script.

# Auto running the script
To make your script run automatically when the server starts, you simply put it into one of these folders. Again, if you have Half-Life 2 Garry's Mod Edition installed somewhere else, navigate there instead.

* For shared scripts ( Loaded on either client or server )


```
/storage/emulated/0/srceng/hl2gmed/lua/autorun
```


* For client-only scripts ( Loaded only on client )


```
/storage/emulated/0/srceng/hl2gmed/lua/autorun/client
```


* For server-only scripts ( Loaded only on server )


```
/storage/emulated/0/srceng/hl2gmed/lua/autorun/server
```


For this specific tutorial, any of those paths will work just fine.

# Loading portions of a script on the client or server
If you want to use a single file for clientside and serverside code, but want separate parts of the code between client and server, we can do something like this:

* To run code only on the client


```lua
if CLIENT then
   --Your clientside code here
end
```


* To run code only on the server


```lua
if SERVER then
   --Your serverside code here
end
```


* To load onto shared (either Client **or** Server), don't specifically check for `CLIENT` or `SERVER`, just put your code down without the `if` block.

Example:


```lua
print( "Hello Shared!" )

if SERVER then
	print( "Hello Server!" )
end

if CLIENT then
	print( "Hello Client!" )
end
```


The `CLIENT` and `SERVER` variables you see up there are explained on the [States](/static/pages/wip.html) page
