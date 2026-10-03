🕳️ Dark Ui V2.5 🕳️

Modern Roblox UI library — dark theme, dark purple-red accents, progressive optional loading, and Proxy-compatible controls (`:Set`, `:SetDescription`).
---
✨ Features
```
| Feature            | Description                                                                               |
| ------------------ | ----------------------------------------------------------------------------------------- |
| 🎨 Dark theme      | Black / gray base with dark purple-red accents                                            |
| 🔘 Floating button | Circular logo button to open / close the UI                                               |
| 🔔 Notifications   | Built-in `Library:Notify`                                                                 |
| 🔍 Search          | Global + page search                                                                      |
| 📑 Tabs & sections | Left / right groupboxes                                                                   |
| ⚡ Rendering        | Optional progressive load (`"true"` / `"false"`)                                          |
| 🧩 Full controls   | Toggle, Button, Slider, Dropdown, Input, KeyBind, Label, Paragraph, Separator, LinkInvite |
```
---
📦 Installation
```lua
local Library = loadstring(game:HttpGet("https://raw.githubusercontent.com/DarkHub-Oficial/Dark-Ui/refs/heads/main/Ui-Library/DarkUiLibraryV2.5.luau"))()
```
Or local file:
```lua
local Library = loadstring(readfile("DarkUiLibraryV2.5.luau"))()
```
---
🚀 Quick Start
```lua
local Library = loadstring(game:HttpGet("https://raw.githubusercontent.com/DarkHub-Oficial/Dark-Ui/refs/heads/main/Ui-Library/DarkUiLibraryV2.5.luau"))()

local Window = Library:CreateWindow({
    Title = "Dark Ui V2.5",
    Desc = "- Example",
    Image = "rbxassetid://127598561744166",
    Rendering = "false"
})

local Tab = Window:AddTab("Main")
local Section = Tab:AddLeftGroupbox("General")

Section:AddToggle("MyToggle", {
    Title = "Enable Feature",
    Default = false,
    Callback = function(Value)
        print(Value)
    end
})
```
---
🪟 CreateWindow
```
| Option      | Type          | Description                                   |
| ----------- | ------------- | --------------------------------------------- |
| `Title`     | string        | Main title                                    |
| `Desc`      | string        | Subtitle                                      |
| `Image`     | string        | Logo (`rbxassetid://...`)                     |
| `Rendering` | string / bool | `"true"` = delayed load · `"false"` = instant |
```
---
📑 Tabs system
```lua
local Tabs = {
    TabMain = "true",
    TabShop = "false"
}

local function IsTab(name)
    local v = Tabs[name]
    return v == true or v == "true"
end

if IsTab("TabMain") then
    local Tab = Window:AddTab("Main")
end
```
✅ `"true"` → tab is created  
❌ `"false"` → tab is skipped
---
🧩 Controls
➕ AddTab
```lua
local Tab = Window:AddTab("Main")
```
📦 AddLeftGroupbox / AddRightGroupbox / AddSection
```lua
local Section = Tab:AddLeftGroupbox("General")
local Section2 = Tab:AddRightGroupbox("Settings")
```
---
🔘 AddToggle
```lua
local Toggle = Section:AddToggle("ToggleId", {
    Title = "Option Name",
    Default = false,
    Callback = function(Value)
        print("Toggle:", Value)
    end
})

Toggle:Set(true)
Toggle:SetValue(false)
print(Toggle:Get())
```
---
🖱️ AddButton
```lua
Section:AddButton({
    Title = "Click Me",
    Callback = function()
        print("Clicked")
    end
})
```
---
📊 AddSlider
```lua
local Slider = Section:AddSlider({
    Title = "Value",
    Min = 100,
    Max = 1000,
    Default = 100,
    Precise = false,
    Callback = function(Value)
        print("Slider:", Value)
    end
})

Slider:Set(500)
```
---
📋 AddDropdown (single)
```lua
Section:AddDropdown("Island", {
    Title = "Select Island",
    Values = {"Island 1", "Island 2", "Island 3"},
    Default = "Island 1",
    Multi = false,
    Callback = function(Value)
        print(Value)
    end
})
```
📋 AddDropdown (multi)
```lua
Section:AddDropdown("MultiIsland", {
    Title = "Select Island",
    Values = {"Island 1", "Island 2", "Island 3"},
    Default = {"Island 1"},
    Multi = true,
    Callback = function(Value)
        print(Value)
    end
})
```
---
⌨️ AddInput
```lua
Section:AddInput("InputId", {
    Title = "Write something",
    Placeholder = "Type here...",
    Default = "",
    Callback = function(Text)
        print(Text)
    end
})
```
---
🎹 AddKeyBind
```lua
Section:AddKeyBind({
    Title = "Menu Key",
    Default = Enum.KeyCode.RightShift,
    Mode = "Toggle",
    Callback = function(Value)
        print("Keybind:", Value)
    end
})
```
---
🏷️ AddLabel
```lua
Section:AddLabel("Status: true")
```
---
📝 AddParagraph
```lua
local Status = Section:AddParagraph("Mirage Island", "Status:❌")

Status:SetDescription("Status:✅")
Status:SetDesc("Status:❌")
Status:SetTitle("Mirage Island")
```
Live example (toggles every 1s):
```lua
local Live = Section:AddParagraph("Server Event", "Status:✅")

task.spawn(function()
    local on = true
    while true do
        task.wait(1)
        on = not on
        Live:SetDescription(on and "Status:✅" or "Status:❌")
    end
end)
```
---
➖ AddSeperator
```lua
Section:AddSeperator("Info")
```
---
🔗 AddLinkInvite
```lua
Section:AddLinkInvite({
    Title = "Discord Invite",
    Banner = "100023306258643",
    Photo = "80861671332748",
    Link = "https://discord.gg/example",
    Button = "Join Server",
    Callback = function(link)
        print(link)
    end
})
```
---
🔔 Notifications
```lua
Library:Notify({
    Title = "Dark Ui V2.5",
    Desc = "UI fully loaded!",
    Duration = 3
})
```
---
🛠️ Other methods
```lua
Library:ToggleUI()
Library:DestroyUI()
```
Floating button (bottom-left) also toggles the UI and is draggable.
---
📐 Full UI example structure
```text
Window (Dark Ui V2.5)
├── 👥 Community
│   └── Invite
│       └── 🔗 AddLinkInvite
├── 🛒 Shop
│   └── Buy
│       ├── 🖱️ Buy Sword / Fight Styles / Guns / Fruits
│       ├── 📋 Select Island (single)
│       └── 🔘 Teleport to Island
├── 🏠 Main
│   └── Teleport
│       ├── 📋 Multi Island
│       ├── 🔘 Teleport Island
│       ├── ➖ Info
│       ├── 📝 Paragraphs
│       ├── 🏷️ Label
│       ├── 📊 Slider
│       ├── ⌨️ Input
│       ├── 🔘 Feature toggles
│       └── 🎹 KeyBind
└── 📡 Status
    └── Live Status
        └── 📝 Paragraph (✅ / ❌ every 1s)
```
---
🧪 Complete example (all controls)
See file: `Dark Ui V2.5 Example.luau`
```lua
local Library = loadstring(game:HttpGet("https://raw.githubusercontent.com/DarkHub-Oficial/Dark-Ui/refs/heads/main/Ui-Library/DarkUiLibraryV2.5.luau"))()

local Window = Library:CreateWindow({
    Title = "Dark Ui V2.5",
    Desc = "- Example",
    Image = "rbxassetid://127598561744166",
    Rendering = "false"
})

local Tabs = {
    TabCommunity = "true",
    TabShop = "true",
    TabMain = "true",
    TabStatus = "true"
}

local function IsTab(name)
    local v = Tabs[name]
    return v == true or v == "true"
end

if IsTab("TabCommunity") then
    local TabCommunity = Window:AddTab("Community")
    local SecInvite = TabCommunity:AddLeftGroupbox("Invite")
    SecInvite:AddLinkInvite({
        Title = "Discord Invite",
        Banner = "100023306258643",
        Photo = "80861671332748",
        Link = "https://discord.gg/example",
        Button = "Join Server",
        Callback = function(link)
            print(link)
        end
    })
end

if IsTab("TabShop") then
    local TabShop = Window:AddTab("Shop")
    local SecShop = TabShop:AddLeftGroupbox("Buy")
    SecShop:AddButton({ Title = "Buy Sword", Callback = function() end })
    SecShop:AddButton({ Title = "Buy Fight Styles", Callback = function() end })
    SecShop:AddButton({ Title = "Buy Guns", Callback = function() end })
    SecShop:AddButton({ Title = "Buy Fruits", Callback = function() end })
    local SelectedIsland = "Island 1"
    SecShop:AddDropdown("SelectIsland", {
        Title = "Select Island",
        Values = {"Island 1", "Island 2", "Island 3", "Island 4"},
        Default = "Island 1",
        Multi = false,
        Callback = function(Value) SelectedIsland = Value end
    })
    SecShop:AddToggle("TeleportIsland", {
        Title = "Teleport to Island",
        Default = false,
        Callback = function(Value)
            if Value then print(SelectedIsland) end
        end
    })
end

if IsTab("TabMain") then
    local TabMain = Window:AddTab("Main")
    local SecMain = TabMain:AddLeftGroupbox("Teleport")
    SecMain:AddDropdown("MultiIsland", {
        Title = "Select Island",
        Values = {"Island 1", "Island 2", "Island 3", "Island 4"},
        Default = {"Island 1"},
        Multi = true,
        Callback = function(Value) end
    })
    SecMain:AddToggle("TeleportMulti", {
        Title = "Teleport Island",
        Default = false,
        Callback = function(Value) end
    })
    SecMain:AddSeperator("Info")
    SecMain:AddParagraph("Example")
    SecMain:AddParagraph("Example:", "Ex\nEx\nEx")
    SecMain:AddLabel("Status: true")
    SecMain:AddSlider({
        Title = "Value",
        Min = 100,
        Max = 1000,
        Default = 100,
        Callback = function(Value) end
    })
    SecMain:AddInput("WriteInput", {
        Title = "Write the He wants",
        Placeholder = "Write the He wants",
        Default = "",
        Callback = function(Text) end
    })
    SecMain:AddToggle("FeatureA", {
        Title = "Feature A",
        Default = false,
        Callback = function(Value) end
    })
    SecMain:AddToggle("FeatureB", {
        Title = "Feature B",
        Default = true,
        Callback = function(Value) end
    })
    SecMain:AddKeyBind({
        Title = "Menu Key",
        Default = Enum.KeyCode.RightShift,
        Callback = function() end
    })
end

if IsTab("TabStatus") then
    local TabStatus = Window:AddTab("Status")
    local SecStatus = TabStatus:AddLeftGroupbox("Live Status")
    local LiveStatus = SecStatus:AddParagraph("Server Event", "Status:✅")
    task.spawn(function()
        local on = true
        while true do
            task.wait(1)
            on = not on
            LiveStatus:SetDescription(on and "Status:✅" or "Status:❌")
        end
    end)
end

Library:Notify({
    Title = "Dark Ui V2.5",
    Desc = "UI fully loaded!",
    Duration = 3
})
```
---
📄 Files
```
| File                                         | Description        |
| -------------------------------------------- | ------------------ |
| `DarkUiLibraryV2.5.luau` / `Ui-Library.luau` | Full UI library    |
| `Dark Ui V2.5 Example.luau`                  | Complete example   |
| `README.md`                                  | This documentation |
```
---
📜 License
Free to use in your hubs and scripts. Credit appreciated but not required.
