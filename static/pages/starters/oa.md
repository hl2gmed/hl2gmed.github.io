HL2 GMod Edition adds a custom operator and aliases various native Lua operators.

| HL2 GMod Edition <br/> Operator | Note |
|:---:|:----------------------------|
| `continue` | Consider using `goto` for `repeat-until` loops instead.

| Lua | HL2 GMod Edition <br/> Alias |
|:---:|:-----------------------:|
| `and` | `&&`
| `or` | `||`
| `not` | `!`
| `~=` | `!=`
| `--[[ ]]` | `/* */`
| `--` | `//`

<div class="warning"><b>⚠️WARNING:</b><br>If you want to keep your code compatible with other Lua environments,  it's recommended to <b>avoid</b> using these custom <b>operators & aliases</b></div>
