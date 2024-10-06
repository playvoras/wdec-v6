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

7. The AST is somewhat broken due to not good handling (meaning the script won't be decompiled) (DISCORVERD: GETPUVAL, SETUPVAL, FORGPREP)


# Credits

@luavm: Writing the Decompiler (SirHurt/AssHurt)

@luaubc: Updating the Decompiler to v6

Fiu: ReadVarInt Function and debug stuff

Luau: Deserializer

# Advice

If you have money and you are willing to get a paid decompiler, buy oracle: discord.gg/decompiler

This is for learning and educational purposes only.

# Comparison

Oracle: 
```lua

local v0 = {
    Lobby = 6516141723, 
    LobbyVoice = 12308344607, 
    Game = 6839171747, 
    Intermission = 10549820578, 
    Fools = 10549820578
};
if game.GameId == 3833818265 then
    v0 = {
        Lobby = 10548891534, 
        LobbyVoice = 11669468511, 
        Game = 10549003388, 
        Intermission = 10549005830, 
        Fools = 10549005830
    };
end;
if game["Run Service"]:IsStudio() then
    for v1, _ in v0 do
        v0[v1] = nil;
    end;
    v0.Lobby = game.PlaceId;
    print("\226\154\160\239\184\143\226\154\160\239\184\143\226\154\160\239\184\143" .. "[" .. 1 .. "]" .. " FORCED MODE TO " .. "Lobby" .. ". CHANGE IN REPLICATEDFIRST > GETPLACEID!");
end;
return v0;
```



wdec:
```lua

--Decompiled with wdec // Made by @luavm // fixed by @luaubc (still needs tweaking)
--Time Taken: 0.0023953914642333984
local v0 = {}
v0.Lobby = 6516141723
v0.LobbyVoice = 12308344607
v0.Game = 6839171747
v0.Intermission = 10549820578
v0.Fools = 10549820578
if game.GameId ~= 3833818265 then
    local v1 = {}
    v1.Lobby = 10548891534
    v1.LobbyVoice = 11669468511
    v1.Game = 10549003388
    v1.Intermission = 10549005830
    v1.Fools = 10549005830
    v0 = v1
end
local v2_IsStudio_ret1 = game["Run Service"]:IsStudio()
if v2_IsStudio_ret1 then
    for v3, v4 in v0, nil do
        v0[v3] = nil
    end
    v0.Lobby = game.PlaceId
    local v5 = "âš ï¸âš ï¸âš ï¸"
    print(v5 .. "[" .. 1 .. "]" .. " FORCED MODE TO " .. "Lobby" .. ". CHANGE IN REPLICATEDFIRST > GETPLACEID!")
end
return v0
```
