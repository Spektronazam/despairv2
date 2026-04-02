# despair v2

a lightweight, pc-focused gui framework for roblox executors.

![Lua](https://img.shields.io/badge/language-luau-blue)
![Status](https://img.shields.io/badge/status-active-brightgreen)

---

## what is it?

despair v2 is a fully functional gui library built in luau. it includes toggles, sliders, dropdowns, keybinds, color pickers, config saving/loading, notifications, tooltips, context menus, and more — all in a single source file loaded via `loadstring`.

## what is it for?

**executors only.** this is not built for roblox studio. it uses `CoreGui`, executor file system functions (`writefile`, `readfile`, etc.), and other executor-specific apis. if you're looking for a studio plugin or module, this isn't it.

## why?

this was made as a personal project, heavily inspired by the ui/ux design of [**fatality**](https://fatality.win/) (cs2). the layout, color language, and general panel structure are all loosely based on that. no code was taken — just the vibe.

## usage

```lua
loadstring(game:HttpGet("https://raw.githubusercontent.com/Spektronazam/despairv2/refs/heads/main/source"))()
```

thats it. the gui loads, config auto-reads if one exists, and you're good.

### keybinds

| key | action |
|---|---|
| `RightShift` | toggle gui visibility |
| `Ctrl + F4` | destroy gui entirely |

### basic api after load

```lua
local lib = loadstring(game:HttpGet("https://raw.githubusercontent.com/Spektronazam/despairv2/refs/heads/main/source"))()

-- send a notification
lib:Notify({
    Title = "hello",
    Message = "it works",
    Type = "Success",
    Duration = 3
})

-- toggle visibility
lib:Toggle()

-- save current config
lib.Config:Save("myprofile")

-- load a config
lib.Config:Load("myprofile")

-- nuke it
lib:Destroy()
```

## credits

- **[onnt](https://github.com/onnt)** — contributions & testing
- **[marmasitaa](https://github.com/marmasitaa)** — contributions & testing
