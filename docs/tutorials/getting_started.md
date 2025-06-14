---
title: Getting Started
layout: default
nav_order: 15
parent: Tutorials
---

# Getting Started
## Creating a DREAMS lua include
Any lua file created in `lua\include\dreams` will automatically be initalized with a global `DREAMS` metatable at runtime. You can override hooks and values on this metatable to change the behaviour of everything ranging from movement to rendering. 

Be sure to name it something unique enough so it won't conflict
{: .note}

DREAMS will be initalized with their filename as there internal name, i.e. to run mydream.lua you would call `ply:SetDream("mydream")`   
  
The bare minimum a DREAM file needs is:
```lua
-- Reloads dreams if file is autorefreshed
if not DREAMS then
	Dreams.LoadDreams()
	return
end

-- Adds a room to dreams (room_name, room_model, dream_data, offset)
-- Rooms are automatically rendered and considered for physics with default hooks
-- Rooms can be accessed under DREAMS.Rooms[room.name] or DREAMS.ListRooms[index]
-- Rooms save the properties of a DreamStruct and are accessible under phys, Marks, Props
DREAMS:AddRoom("rainhallway", "models/rooms/rain_hallway.mdl", "data_static/dreams/test/rain_hallway.dat", Vector(10, 10, -100))

-- Variables used by the default StartMove Hooks
DREAMS.MoveSpeed = 40
DREAMS.ShiftSpeed = 40
DREAMS.JumpPower = 400
DREAMS.Gravity = 600
DREAMS.Debug = 0 -- Set to 1 to show bounding boxes for physics

-- Define hooks here
-- function DREAMS:ThinkSelf()
-- end
```

* * *

## Creating DREAM data files
DREAM data files are converted from other file types (currently VMF only) and can easily done so with console commands in-game  

To convert from a VMF, use `dreams_convertvmf <vmf filepath>`, the console will automatically list VMFs in the `maps/*` folder   
An example VMF has been provided in the GitHub repo that demonstrates DREAMS features and will be used during this tutorials and others

If successful, the console should print:
```
[DREAMS] Generated Blender USD Light Data @ garrysmod/data/dreams/rain_hallway.usd.txt -- If lights are present
[DREAMS] Generated Dream DATFILE @ garrysmod/data/dreams/rain_hallway.dat
```
The first file is for baking lights in Blender, the second is your DREAM file.

Place the DREAM file in your addons `data_static/` folder in a place where it won't conflict, then update the dream_data parameter to match the filepath   
   
Setting `DEBUG` to 1 and running `lua_run player.GetAll()[1]:SetDream("mydream")` should show your DreamsPhys model:   
     
![gs_vmf]({{ site.baseurl }}/assets/images/gs_vmf.jpg)