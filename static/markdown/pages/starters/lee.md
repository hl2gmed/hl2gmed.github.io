# What Are Lua Errors?
A Lua error is caused when the code that is being ran is improper. There are many reasons for why a Lua error might occur, but understanding what a Lua error is and how to read it is an important skill that any developer needs to have.

# Effects of Errors on Your Scripts
An error will halt your script's execution when it happens. That means that when an error is thrown, some elements of your script might break entirely. For example, if your gamemode has a syntax error which prevents init.lua from executing, your entire gamemode will break.

# Lua Error Format
The first line of the Lua error contains 3 important pieces of information:

  * The path to the file that is causing the error
  * The line that is causing the error
  * The error itself

Here is an example of a code that will cause a Lua error:
```lua
local text = "Hello World"
Print( text )
```
The code will produce the following error:
```lua
[ERROR]addons/my_addon/lua/autorun/server/sv_my_addon_autorun.lua:2: attempt to call global 'Print' (a nil value)
 1. unknown - addons/my_addon/lua/autorun/server/sv_my_addon_autorun.lua:2
```
