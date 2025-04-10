---
title: Creating a Dreams Model from VMF
layout: default
nav_order: 100
---

# Requirements
These tools are needed to generate models and bake their lighting
* [Blender](https://www.blender.org/) 4.0 or higher
* [Hammer++](https://ficool2.github.io/HammerPlusPlus-Website/download.html) latest version

# Getting Started
Install both of the requirements if you haven't already  
With Dreams, most rooms are created out of props for the models, and a predefined list of polygon solids for physics.  
First thing you need to do is create a room. `rain_hallway.vmf` is provided in the GitHub release as an example if you need something to just follow along.  
After creating your room, make sure your VMF file is saved somewhere in your garrysmod/maps/ folder; This is important for the future steps.
   
## VMF Collision and Entities
Any face that is not textured NoDraw will be considered when converting to physics, i.e. PlayerClips, Hints, etc. and should be removed if needed. Its good practice to also create a separate VMF from the Propper Model for the physics model, as this will allow you fine-tune the models collision without losing the source to your prop model.

In your VMF you can include (entities not listed will simply be ignored): 
* light and light_spot, 
* info_teleport_destination, 
* and info_target entities   
     
light and light_spot ents will be used by the VMF converter to create a Universal Scene Description file containing lighting information, which can be imported into Blender (see below)
        
info_teleport_destination and info_target will provide variables `pos`, `angle`, and `pos` respectively. After creating a room, these can be accessed on the `Marks` table with the key being the same as the `targetname` of the entities. These are good for setting start points or positioning entities

# Creating a Propper Model

# Converting to .phy and .usd
With Dreams installed and enabled in your Garry's Mod, open and launch a Singleplayer or Multiplayer game.  
Open the console and type `dreams_convertfile` and you should see autocomplete options for VMFs in your `maps` folder.  
   
Type the path to the VMF you'd like to convert and press enter. Dreams should print two lines that look like this:
```
DREAMS: Generated Blender USD Light Data garrysmod/data/dreams/rain_hallway.usd.txt -- (only if you had lights in your vmf)
DREAMS: Generated DREAMINFO bin garrysmod/data/dreams/rain_hallway.dat
```
Navigate to your `garrysmod/data/dreams` folder and find the listed files.  
Rename the `.dat` folder to `.phy`, and add an ending (such as '_dream.phy') to differentiate it from your Propper's .phy model. Place it in a folder under `models/` of your choosing, preferably with the model itself.   
`With recent GMod updates, dream files can also be placed in the data_static/ folder as .dat, which may be more preferable for Workshop uploads`  
Remove the .txt from the `.usd.txt` file and set it aside for later.