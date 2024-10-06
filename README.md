# wdec v6

This is a Luau Bytecode Decompiler made by @luavm that decompiles luau bytecode to human-readable Source.

# Usage
```lua
game_httpget = function(s)
  return game:HttpGet(s)
end
local httpget = httpget or game_httpget or http_get -- add your httpget func here
loadstring(httpget("https://raw.githubusercontent.com/Arch-Foundation/wdec-v6/refs/heads/main/lua.luau"))()
decompile(script_path)
```
Replace script_path with whatever script you want to decompile.

You can pair it with writefile or setclipboard etc
e.x
```lua
setclipboard(decompile(game.ReplicatedStorage.ExampleScript))
```

# Flaws
There are multiple flaws with this decompiler:

~~1. The opcode list is not updated.~~

2. AST is partially broken: Reason: not all opcodes are supported and some have even changed behaviour, meaning they need a fix

~~3. Unhandled Opcodes: Due to the Opcode list not being complete, the deserializer can't pick out an invalid table index, so the decompiler (deserializer) errors.~~ Updated

3. Some opcodes not handled: TODO: Handle all opcodes.
 
4. Deprecated Opcodes: This list includes Deprecated opcodes.
 
~~5. BuiltIns are not complete, meaning not all functions can be retrieved.~~ Updated (maybe?)

5. Loops are also not present. (discovered: while .. do)

6. Instead of having else or elseif, the decompiler registers it as another statement so TODO: add reasonable else amnd elseif

7. The AST is somewhat broken due to not good handling (meaning the script won't be decompiled)


# Credits

@luavm: Writing the Decompiler (SirHurt/AssHurt)

@luaubc: Updating the Decompiler to v6

Fiu: ReadVarInt Function and debug stuff

Luau: Deserializer
