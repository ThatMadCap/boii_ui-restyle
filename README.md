# BOII | Development - Utility: UI Elements

---
### Action Menu Restyle
![Screenshot_1](https://github.com/user-attachments/assets/aeb6c237-c466-43e8-9411-5c48f5456366)

<summary>Action Menu Snippet (Click to Expand)</summary>
<details>

```lua
-- Here's a snippet for a test menu
-- "F1" to open the menu (requires ox_lib)
-- or use the command "/boii_radial_test"

local test_menu = {
  {
      label = 'Level 1',
      icon = 'fa-solid fa-sitemap',
      colour = 'red',
      submenu = {
          {
              label = 'Level 2',
              icon = 'fa-solid fa-crown',
              colour = 'pink',
              submenu = {
                  {
                      label = 'Level 3',
                      icon = 'fa-solid fa-truck-moving',
                      colour = 'yellow',
                      submenu = {
                          {
                              label = 'Level 4',
                              icon = 'fa-solid fa-boxes',
                              colour = 'green',
                              submenu = {
                                  {
                                      label = 'Level 5',
                                      icon = 'fa-solid fa-map-marked-alt',
                                      colour = 'blue',
                                      submenu = {
                                          {
                                              label = 'Confirm',
                                              icon = 'fa-solid fa-check-circle',
                                              colour = 'purple',
                                              action_type = 'client',
                                              action = 'example_event',
                                              params = { example_param = 'example_value' }
                                          }
                                      }
                                  }
                              }
                          }
                      }
                  }
              }
          }
      }
  },
  {
      label = 'Police',
      icon = 'fa-solid fa-sitemap',
      submenu = {
          {
              label = 'Fingerprint',
              icon = 'fa-solid fa-shield-halved',
              colour = '#000000', -- hex
              action_type = 'client',
              action = 'example_event',
              params = { example_param = 'example_value' }
          },
          {
              label = 'Handcuff',
              icon = 'fa-solid fa-handcuffs',
              colour = '#FF5733', -- hex
              action_type = 'client',
              action = 'example_event',
              params = { example_param = 'example_value' }
          },
          {
              label = 'Jail',
              icon = 'fa-solid fa-bus',
              colour = 'purple', -- named colour
              action_type = 'client',
              action = 'example_event',
              params = { example_param = 'example_value' }
          },
          {
              label = 'Frisk',
              icon = 'fa-solid fa-hand',
              colour = 'rgb(0, 128, 255, 150)', -- rgb/rgba
              action_type = 'client',
              action = 'example_event',
              params = { example_param = 'example_value' }
          },
          {
              label = 'Search',
              icon = 'fa-solid fa-magnifying-glass',
              colour = 'hsl(200, 100%, 50%)', -- hsl/hsla
              action_type = 'client',
              action = 'example_event',
              params = { example_param = 'example_value' }
          },
          {
              label = 'Covert Operations',
              icon = 'fa-solid fa-person-military-rifle',
              colour = 'black',
              submenu = {
                  {
                      label = 'Raid Container',
                      icon = 'fa-solid fa-box-archive',
                      colour = 'black',
                      action_type = 'client',
                      action = 'example_event',
                      params = { example_param = 'example_value' }
                  },
                  {
                      label = 'Overthrow the Government',
                      icon = 'fa-solid fa-person-rifle',
                      colour = 'red',
                      action_type = 'client',
                      action = 'example_event',
                      params = { example_param = 'example_value' }
                  }
              }
          }
      }
  }
}


local isOpen = false
local isDisabled = false

local function hideRadial()
	if not isOpen then return end
	lib.resetNuiFocus()
	isOpen = false
end

local function disableRadial(state)
    isDisabled = state

    if isOpen and state then
        return hideRadial()
    end
end

lib.addKeybind({
	name = 'boii_ui_radial',
	description = "Open boii_ui Radial Menu",
	defaultKey = 'f1',
	onPressed = function()
    	if isDisabled then return end

    	if isOpen then return end

		if IsNuiFocused() or IsPauseMenuActive() then return end

    	isOpen = true

    	lib.setNuiFocus(true)
    	SetCursorLocation(0.5, 0.5)

		-- open action menu
    	exports.boii_ui:action_menu(test_menu)

    	while isOpen do
    		DisablePlayerFiring(cache.playerId, true)
    		DisableControlAction(0, 1, true)
    		DisableControlAction(0, 2, true)
    		DisableControlAction(0, 142, true)
    		DisableControlAction(2, 199, true)
    		DisableControlAction(2, 200, true)
    		Wait(0)
    	end
	end,
	onReleased = function()
		hideRadial()
	end
})

RegisterCommand('boii_radial_test', function()
	SetNuiFocus(true, true)
	exports.boii_ui:action_menu(test_menu)
end, false)
```

</details>

---

Introducing our comprehensive UI Suite designed to enhance roleplay and interaction within your FiveM server. 

This resource includes a set of essential UI elements:
```
Notifications: Visual alerts with customizable styles for informing players of in-game events, warnings, and confirmations.
Progress Bars: Dynamic bars to visually represent the completion of actions or tasks.
Context Menus: An extensive and detailed menu system for deeper interaction with the game environment and objects.
Draw Text UI: On-screen text display for instructions, descriptions, or narrative storytelling.
Dialogue System: An immersive system for engaging player-to-NPC or player-to-player conversations.
```
Our toolkit is built to be intuitive, offering high customizability even for those with minimal coding expertise. The modular design ensures seamless integration with a variety of frameworks and setups. 
Detailed installation instructions are included for effortless implementation.

**Features**

```
Standalone Operation: No dependencies required, ensuring easy plug-and-play functionality.
Developer Friendly: Customization-centric approach with extensive documentation for all UI components.
Immersive Experience: Crafted to provide a rich and engaging user interface, elevating the in-game interaction.
```

### Dependencies

- None script is entirely standalone

### Install

1. **Script Customisation**:
   
   - You can customise the default styles throughout the javascript classes these are all stored within the constructor aside for the notifications.

2. **Script Installation**:

   - Import `boii_ui` into your server resource and ensure the load order is correct. UI resource should be started before any other resource using it.

2. **Restart Server**:
   
   - Having followed the above steps, restart your server, and voilà! Your Job Center utility should be up and running.

### Documentation
https://docs.boii.dev/fivem/free-resources/boii_ui

### PREVIEW
https://www.youtube.com/watch?v=8ga-YqNp9U0

### SUPPORT
https://discord.gg/boiidevelopment
