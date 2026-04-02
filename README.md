<div align="center">

# Despair

minimal ui library for roblox executors

</div>

---

## Introduction

Despair is a single-script UI library for Roblox exploit environments. It's strict-typed, memory-safe, and follows the sUNC standard. Load it, build a window, done.

---

## What Is It

A draggable window with folders containing toggles, sliders, dropdowns, color pickers, keybinds, text inputs, buttons, labels, and separators. Comes with a notification system and JSON config saving built in.

---

## How Does It Work

1. You load the script via `loadstring`
2. It parents a ScreenGui into `gethui()` (or falls back to CoreGui/PlayerGui)
3. Every connection and instance is tracked by an internal maid — calling `:Destroy()` cleans up everything
4. Configs serialize all flags to JSON files in a `Despair/` folder on your executor's filesystem

---

## What Executors Does It Support

Any executor that implements sUNC-standard globals. This includes but isn't limited to:

- Delta
- Xeno
- Wave
- Solara
- Trigon Evo
- Arceus X Neo
- Cryptic
- FluxusZ

If your executor has `gethui`, `cloneref`, and the sUNC filesystem functions, it works.

---

## Is Owner Cute

yes

---

## Example Script

```lua
local Despair = loadstring(game:HttpGet("https://raw.githubusercontent.com/Spektronazam/despairv2/refs/heads/main/source"))()

local win = Despair:Window("Despair — Demo")

-- movement
local movement = win:Folder("Movement")

movement:Toggle({
    name = "Speed Boost",
    default = false,
    flag = "speed_enabled",
    callback = function(state)
        print("Speed:", state)
    end,
})

movement:Slider({
    name = "Walk Speed",
    min = 16,
    max = 200,
    default = 16,
    step = 1,
    flag = "walk_speed",
    callback = function(val)
        game.Players.LocalPlayer.Character.Humanoid.WalkSpeed = val
    end,
})

movement:Bind({
    name = "Fly Key",
    default = Enum.KeyCode.F,
    flag = "fly_key",
    callback = function(key)
        print("Fly pressed:", key.Name)
    end,
})

-- visuals
local visuals = win:Folder("Visuals")

visuals:Color({
    name = "ESP Color",
    default = Color3.fromRGB(40, 165, 225),
    flag = "esp_color",
    callback = function(col)
        print("Color:", col:ToHex())
    end,
})

visuals:Dropdown({
    name = "ESP Mode",
    items = { "Box", "Corner", "Highlight", "Off" },
    default = "Box",
    flag = "esp_mode",
    callback = function(sel)
        print("Mode:", sel)
    end,
})

visuals:Toggle({
    name = "Tracers",
    default = true,
    flag = "tracers",
})

-- misc
local misc = win:Folder("Misc")

misc:Input({
    name = "Target",
    placeholder = "username...",
    flag = "target_name",
    callback = function(text)
        print("Target:", text)
    end,
})

misc:Label("Despair — built different")
misc:Sep()

misc:Button({
    name = "Save Config",
    callback = function()
        Despair.Config.Save("default")
        Despair:Notify({ msg = "Config saved.", type = "success", duration = 2 })
    end,
})

misc:Button({
    name = "Load Config",
    callback = function()
        Despair.Config.Load("default")
        Despair:Notify({ msg = "Config loaded.", type = "info", duration = 2 })
    end,
})

win:Button({
    name = "Destroy UI",
    callback = function()
        win:Destroy()
    end,
})
```

---

## How to Use

**Load it**
```lua
local Despair = loadstring(game:HttpGet("https://raw.githubusercontent.com/Spektronazam/despairv2/refs/heads/main/source"))()
```

**Make a window**
```lua
local win = Despair:Window("Title")
```

**Make folders**
```lua
local folder = win:Folder("Section")
```

**Add elements** — every element takes a table with `name`, `flag`, `callback`, and `default`

```lua
-- toggle
folder:Toggle({ name = "Thing", default = false, flag = "thing", callback = function(v) end })

-- slider
folder:Slider({ name = "Speed", min = 0, max = 100, default = 50, step = 1, flag = "spd", callback = function(v) end })

-- dropdown
folder:Dropdown({ name = "Mode", items = {"A", "B"}, default = "A", flag = "mode", callback = function(v) end })

-- color picker
folder:Color({ name = "Color", default = Color3.fromRGB(255, 0, 0), flag = "col", callback = function(v) end })

-- keybind
folder:Bind({ name = "Key", default = Enum.KeyCode.E, flag = "key", callback = function(v) end })

-- text input
folder:Input({ name = "Name", placeholder = "...", flag = "name", callback = function(v) end })

-- button
folder:Button({ name = "Run", callback = function() end })

-- label
local lbl = folder:Label("text")
lbl:Set("new text")

-- separator
folder:Sep()
```

**Read flags anytime**
```lua
print(Despair.flags.thing)   -- boolean
print(Despair.flags.spd)     -- number
print(Despair.flags.col)     -- Color3
```

**Configs**
```lua
Despair.Config.Save("name")     -- saves to Despair/name.json
Despair.Config.Load("name")     -- loads flags from file
Despair.Config.Delete("name")   -- deletes config file
Despair.Config.List()            -- returns { "name", ... }
```

**Notifications**
```lua
Despair:Notify({ msg = "hello", type = "info", duration = 3 })
-- types: "info", "success", "warn", "error"
```

**Cleanup**
```lua
win:Destroy()
```

---

## Credits

**spekT** — author, design, architecture

**steel** — contributions, testing

---

<div align="center">
<sub>despair · 2026</sub>
</div>
