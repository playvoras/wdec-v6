# Uses

Loading the Decompiler Function to Variable: 

Executor: 
```lua
local decompile = loadstring(game:HttpGet("https://raw.githubusercontent.com/Arch-Foundation/wdec-v6/refs/heads/main/scripts/load_decomp.lua"))()
```

# Ways to decompile

Saving Script to file

```lua
--// .. Decompile Script on top
local script_path = nil -- replace this with your script path
writefile(script_path.Name .. " Decompiled", decompile(script_path))
```

print/error/warn
```lua
--// .. Decompile Script on top
local desired_func = print
local script_path = nil -- replace this with your script path
desired_func(script_path.Name .. " Decompiled", decompile(script_path))
```

saveinstance: Copy the decompiler script (HAS TO BE ON TOP) then the saveinstance script at the bottom (might release a decompiler dedicated one tbh)
