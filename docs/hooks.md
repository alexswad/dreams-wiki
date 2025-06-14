---
title: Hooks
layout: default
nav_order: 5
---
Hooks that can be overriden on the DREAMS metatable
- TOC
{:toc}

## SERVER
### DREAMS:ThinkSelf
{: .d-inline }
()
{: .d-inline .fs-5 .text-purple-200 }
SERVER
{: .label .label-blue }
Called before any player think, allows for updating ent positions & dream variables  

* * *

### DREAMS:EntityTakeDamage
{: .d-inline }
(ply, attacker, inflictor, dmg)
{: .d-inline .fs-5 .text-purple-200 }
SERVER
{: .label .label-blue }
Called when the player takes damage from anything, including things outside of Dreams    
Return `true` to block
```lua 
return Dreams.Meta.EntityTakeDamage(self, ply, attacker, inflictor, dmg) 
```
- Will prevent anything but players in dreams from hurting other dreaming players

* * *

## CLIENT
### DREAMS:Draw
{: .d-inline }
(ply: LocalPlayer)
{: .d-inline .fs-5 .text-purple-200 }
CLIENT
{: .label .label-yellow }
Called during RenderScene after SetupFog and CalcView, provides a 3D camera space. Draw other clientside models or effects here  
```lua 
Dreams.Meta.Draw(self, ply, DEBUG)
```
- Automatically draws the room the player is in and other players  
- DEBUG will draw the bounding boxes of all solids if set to 1, Face normals if set to 2, and Face Normals and the Bounding Boxes if set to 3

* * *

### DREAMS:DrawHUD
{: .d-inline }
(ply: LocalPlayer, w, h)
{: .d-inline .fs-5 .text-purple-200 }
CLIENT
{: .label .label-yellow }
Called during RenderScene after all other render hooks and provides a 2D camera space   


```lua
Dreams.Meta.DrawHUD(self, ply, w, h)
```

* * *

### DREAMS:HUDShouldDraw
{: .d-inline }
(ply: LocalPlayer, HUDElement: str)
{: .d-inline .fs-5 .text-purple-200 }
CLIENT
{: .label .label-yellow }
Allows you to prevent default HUD elements from being rendered. See [GM:HUDShouldDraw](https://wiki.facepunch.com/gmod/GM:HUDShouldDraw)   
Return `false` to prevent drawing the element   
* * *

### DREAMS:CalcView
{: .d-inline }
(ply: LocalPlayer, view: table)
{: .d-inline .fs-5 .text-purple-200 }
CLIENT
{: .label .label-yellow }
Calculates the players view position by edting the table, see [Structures/CamData](https://wiki.facepunch.com/gmod/Structures/CamData)   
```lua 
Dreams.Meta.CalcView(self, ply, view) --(no return necessary)
```
- Calculates the players view at their position with the default height (64 hmu)

* * *

### DREAMS:RenderScene
{: .d-inline }
(ply: LocalPlayer)
{: .d-inline .fs-5 .text-purple-200 }
CLIENT
{: .label .label-yellow }
Draws Dreams in it's entirety. You can do more advanced post processing effects here 
```lua
function DREAMS:RenderScene(ply)
	local view = {
		origin = origin,
		angles = angles,
		fov = fov,
	}
	if not self:SetupFog(ply) then render.FogMode(MATERIAL_FOG_NONE) end
	self:CalcView(ply, view)
	cam.Start3D(view.origin, view.angles, view.fov, 0, 0, ScrW(), ScrH())
	self:Draw(ply)
	cam.End3D()

	cam.Start2D()
	self:DrawHUD(ply, ScrW(), ScrH())
	cam.End2D()
	return true
end
```

* * *

### DREAMS:SetupFog
{: .d-inline }
(ply: LocalPlayer) 
{: .d-inline .fs-5 .text-purple-200 }
CLIENT
{: .label .label-yellow }
Works like GM:SetupWorldFog(), use render.Fog* functions and return `true` to finish setting up fog   

* * *

### DREAMS:EntityEmitSound
{: .d-inline }
(tbl)
{: .d-inline .fs-5 .text-purple-200 }
CLIENT
{: .label .label-yellow }
Allows manipulation of clientside sounds while dreaming. Return `false` to prevent  
See [GM:EntityEmitSound](https://wiki.facepunch.com/gmod/GM:EntityEmitSound)   
Due to EmitSounds limitations, not all sounds can be accessed or prevented, which is extremely unfortunate    
```lua
return Dreams.Meta.EntityEmitSound(self, tbl)
```
- Will prevent all sounds except those emitted from LocalPlayer()

* * *

## SHARED
### DREAMS:Think
{: .d-inline }
(ply)
{: .d-inline .fs-5 .text-purple-200 }
SHARED
{: .label .label-purple }
Called once for every player on Server and the LocalPlayer on Client during the Think hook

* * *

### DREAMS:Start
{: .d-inline }
(ply)
{: .d-inline .fs-5 .text-purple-200 }
SHARED
{: .label .label-purple }
Called when a player starts a dream on Server or the LocalPlayer on Client. Responsible for player setup serverside   
```lua 
Dreams.Meta.Start(self, ply)
```
- Setups the player's positioning in the real world so the player can be networked. You would normally want to call this unless you know what your doing

* * *

### DREAMS:End
{: .d-inline }
(ply)
{: .d-inline .fs-5 .text-purple-200 }
SHARED
{: .label .label-purple }
Called when a player ends a dream on Server or the LocalPlayer on Client.

* * *

### DREAMS:SwitchWeapon
{: .d-inline }
(ply, old, new)
{: .d-inline .fs-5 .text-purple-200 }
SHARED
{: .label .label-purple }
{: .d-inline }
PREDICTED
{: .label .label-green }
Return `true` to prevent the player from switching their weapon. Switching to nothing will still call this hook   
```lua 
Dreams.Meta.SwitchWeapon(self, ply, old, new)
```
- Prevents the player from switching to anything except nothing

* * *

### DREAMS:SetupDataTables
{: .d-inline }
()
{: .d-inline .fs-5 .text-purple-200 }
SHARED
{: .label .label-purple }
If defined, will automatically create a DREAMS.NetEntity for easy networking.   
Will be available right before DREAMS:Init() and re-created if cleaned up  
Use [self:NetworkVar(type, slot, name)](https://wiki.facepunch.com/gmod/Entity:NetworkVar) to create Get(name) & Set(name) functions  


Int Slot 31 is reserved to mark the dreams_entity to the associated dream
{: .note }
* * *

## Move Hooks
### DREAMS:StartMove
{: .d-inline }
(ply, mv, cmd)
{: .d-inline .fs-5 .text-purple-200 }
SHARED
{: .label .label-purple }
{: .d-inline }
PREDICTED
{: .label .label-green }
Called at the start of a move command, setup the players velocity and process their input here.    
Must return `true`          
See [GM:SetupMove](https://wiki.facepunch.com/gmod/GM:SetupMove)       
- StartMove can be replaced with DREAMS.StartMoveFly ex. `DREAMS.StartMove = DREAMS.StartMoveFly` either for debugging or for gameplay
- Dreams.Meta.StartMove can be called with extra parameters `jump` and `grav` to override DREAMS default values
### DREAMS:DoMove
{: .d-inline }
(ply, mv)
{: .d-inline .fs-5 .text-purple-200 }
SHARED
{: .label .label-purple }
{: .d-inline }
PREDICTED
{: .label .label-green }
Called to setup the origin of a move command, all collisions are done here.

### DREAMS:FinishMove
{: .d-inline }
(ply, mv)
{: .d-inline .fs-5 .text-purple-200 }
SHARED
{: .label .label-purple }
{: .d-inline }
PREDICTED
{: .label .label-green }
Called to set movement data to the player