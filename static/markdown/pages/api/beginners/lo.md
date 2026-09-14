#  Getting Started — Lua Loading Order<hr>

This list shows the order of loading Lua files in Half-Life 2 Garry's Mod Edition.

<div class="note"><b>💡NOTE:</b><br><i>HL2GMed combines all scripts into a virtual filesystem (one folder). addon/myaddon/lua/entities/ and gamemodes/base/gamemode/entities/entities/ will be merged with lua/entities/, so therefore the same path and name will override and/or conflict.</i></div>
<div class="note"><b>💡NOTE:</b><br><i>Autorun lua files are sorted alphabetically(A-Z) on all OSes before being executed</i></div>

# Client loading order

- `includes/init.lua` - Everything from `includes/` is included from this file

- `gamemodes/base/gamemode/cl_init.lua` - Everything from `gamemodes/base/gamemode/` is included from this file

- `autorun/`

  - `autorun/client/`

- `postprocess/`

- `vgui/`

- `gamemodes/*gamemodename*/gamemode/cl_init.lua` - Everything from `gamemodes/*gamemodename*/gamemode/` is included from this file

- `weapons/`

  - `weapons/hl2gmed_tool/stools/`

- `entities/`

# Server loading order

- `includes/init.lua` - Everything from `includes/` is included from this file

- `gamemodes/base/gamemode/init.lua` - Everything from `gamemodes/base/gamemode/` is included from this file

- `autorun/`

  - `autorun/server/`

  - `autorun/server/sensorbones`

- `includes/dev_server_test.lua` - Only executed if the `-systemtest` command line parameters were added.

- `gamemodes/*gamemodename*/gamemode/init.lua` - Everything from `gamemodes/*gamemodename*/gamemode/` is included from this file

- `weapons/`

  - `weapons/hl2gmed_tool/stools/`

- `entities/`
