# Global Variables
## Global Tabels
There are various global tables containing the active game
state some of which are only available in specific scopes.
<table>
<thead>
<tr>
<th>Variable</th>
<th>Value</th>
<th>Scope</th>
</tr>
</thead>
<tbody>
<tr>
<td>GAMEMODE</td>
<td>The active gamemode</td>
<td>Available anywhere
Only available if the gamemode has been loaded</td>
</tr>
<tr>
<td>GM</td>
<td>The loading gamemode</td>
<td>Available inside the gamemode's files
Only available while the gamemode is loading

gamemodes/<Gamemode>/gamemode/*.lua</td>
</tr>
<tr>
<td>ENT</td>
<td>The current scripted entity</td>
<td>Available inside the entity's files

lua/entities/*.lua</td>
</tr>
<tr>
<td>NPC</td>
<td>The current scripted npc</td>
<td>Available inside the npc's files

lua/npcs/*.lua</td>
</tr>
<tr>
<td>SWEP</td>
<td>The current scripted weapon</td>
<td>Available inside the weapon's files

lua/weapons/*.lua</td>
</tr>
<tr>
<td>_G</td>
<td>All globals, including itself</td>
<td>Available anywhere</td>
</tr>
<tr>
<td>_MODULES</td>
<td>List of all /modules/</td>
<td>Available anywhere</td>
</tr>
<tr>
</tr>
</tbody>
