---
title: VMF Library
layout: default
nav_order: 20
parent: Functions
---
Functions under Dreams.VMF.*
- TOC
{:toc}

### VMF.ConvertFile(file_name)
Returns a DreamStruct table that can be saved for later
```lua
{
	phys = DreamPhys
	marks = { ...{[pos] = Vector, [angles] = Angle} }
	--props = tbd
	lights = { ...{
		color = Color
		name = string
		pos = Vector
		angles = Angles
		cone = integer
	}}
}
```

### VMF.ExtractEnts(vmf_string)
Returns the raw table of entities from a VMF

### VMF.ExtractSolids(vmf_string)
Returns the raw table of solids froms a VMF

### VMF.SolidToPhys(solid_table)
Returns a table containing the converted solid to DreamPhys Solid

### VMF.ConvertLightEntity(light_table)
Returns a table containing the parsed light data

### VMF.SaveLights(fname, lights_table)
Saves parsed lights to a .usd file in `data/dreams/<fname>.usd.txt`