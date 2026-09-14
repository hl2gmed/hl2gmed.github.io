#  Getting Started — Error Explaination<hr>

#  What Are Lua Errors? 
A Lua error is caused when the code that is being ran is improper. There are many reasons for why a Lua error might occur, but understanding what a Lua error is and how to read it is an important skill that any developer needs to have.

#  Effects of Errors on Your Scripts 
An error will halt your script's execution when it happens. That means that when an error is thrown, some elements of your script might break entirely. For example, if your gamemode has a syntax error which prevents init.lua from executing, your entire gamemode will break.

#  Lua Error Format 
The first line of the Lua error contains 3 important pieces of information:
* The path to the file that is causing the error
* The line that is causing the error
* The error itself

Here is an example of a code that will cause a Lua error:


```
local text = "Hello World"
Print( text )
```


The code will produce the following error:


```
[ERROR]addons/my_addon/lua/autorun/server/sv_my_addon_autorun.lua:2: attempt to call global 'Print' (a nil value)
 1. unknown - addons/my_addon/lua/autorun/server/sv_my_addon_autorun.lua:2
```


That is because **Print** is not an existing function (**print**, however, does exist).

The first line includes the path to the file that is causing the error - **addons/my_addon/lua/autorun/server/sv_my_addon_autorun.lua**

Afterwards, the line that's producing the error - **sv_my_addon_autorun.lua:2** (Line 2)

Lastly, the error itself - **attempt to call global 'Print' (a nil value)**

Below the error, we have the trace of the function. Simplified - If the error is inside a function/chunk of code that is called from somewhere else, it will state where the code is called from.

If the error happens serverside, the text color will be blue. If it happened clientside, it will be yellow. If it's menu code, it will be green (not a typical scenario). Messages which look like errors but are colored differently, such as red or white, are not Lua errors but rather engine errors.

# Common Errors 

## Attempt to call global '?' a nil value 

**Description:** You tried to call a function that doesn't exist.

**Possible causes:** 
* Your function might be defined in another Lua state. (e.g Calling a function on the client that only exists on the * server.)
* You're using a metafunction on the wrong kind of object. (e.g. Calling :SteamID() on a Vector)
* The function you're calling has an error in it which means it is not defined.
* You've misspelled the name of the function.

**Ways to fix:**
* Make sure the function exists
* Make sure your function is defined in the correct realm
* Check your function calls for spelling errors


## Attempt to perform arithmetic on global '?' (a nil value) 

**Description:** You tried to perform arithmetic (+, -, *, /) on a global variable that is not defined.

**Possible causes:** 
* You tried to use a local variable that was defined later in the code
* You've misspelled the name of the global variable

**Ways to fix:**
* Make sure you define local variables before calling them in the code
* Check for spelling errors


## Attempt to perform arithmetic on '?' (a type value) 

**Description:** You tried to perform arithmetic (+, -, *, /) on a variable that cannot perform arithmetic. (e.g. 2 + "some string")


## Attempt to index global 'varname' (a nil value) 

**Description:** You tried to index an undefined variable (e.g. `print( variable.index )` where `variable` is undefined)

**Possible causes:**
* The variable is defined in a different realm
* The variable is local and defined later in the code
* You've misspelled the name of the variable

**Ways to fix:**
* Make sure the variable is only accessed in the realm it was defined in
* If the variable is local, define it before accessing it


## Malformed number near 'number' 

**Description:** There is a malformed number in the code (e.g. 1.2.3, 2f) 

**Possible causes:**
* An IP address was written as a number instead of a string
* Incorrect writing of multiplication of a number and a variable
* Trying to concatenate a number to a string without a space between the number and the operator.

**Ways to fix:**
* Store IP addresses as a string
* Multiply variables with numbers by using the ***** operator
* Put a space between the concat (**..**) operator and the number.


## Unexpected symbol near 'symbol' 

**Description:** You typed a symbol in the code that Lua didn't know how to interpret.

**Possible causes:**
* Incorrect syntax (e.g. Forgot to write "then" after an if statement)
* Not closing brackets and parentheses at the correct locations

**Ways to fix:**
* Make sure there are no mistypes in the code
* Close brackets and parentheses correctly (See: Code Indentation)


## 'symbol1' expected near 'symbol2' 
**Description:** Lua expected symbol1 instead of symbol2.
When 'symbol2' is <eof>, Lua expected a symbol before the end of the file

**Possible causes:**
* Not closing all brackets, parentheses or functions before the end of the file
* Having too many `end` statements
* Wrong operator calling (e.g. "==" instead of "=")
* Missing comma after table item.

**Ways to fix:**
* Close brackets and parentheses correctly (See: Code Indentation)
* Use the correct operators
* Add a comma after a table item

## Couldn't include file 'file' - File not found (<nowhere>)
**Description:** The file system tried to include a file that either doesn't exist or was added while the server was live.

**Possible causes:**
* Attempting to include a file that doesn't exist or is empty
* Creating a file while the server is still live

**Ways to fix:**
* Add the non-existent file, make sure the file isn't empty
* Restart the server
