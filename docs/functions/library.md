---
title: General Library
layout: default
nav_order: 15
parent: Functions
---

## Physics / Intersections
### lib.MagnitudeToNormal
{: .d-inline-block }
(xdelta: float, ydelta: float, zdelta: float)
{: .d-inline .fs-4 .text-blue-100 }

Returns the `normal: Vector` facing the direction of the axis of the highest magnitude   
Used by Cylinder and Sphere intersections   
`delta` variables use their absolute value internally   

### lib.IntersectABCylinderWithAABB
{: .d-inline-block }
(cylOrg: Vector, cylRadius: float, cylHeight: float, boxmin: Vector, boxmax: Vector)
{: .d-inline .fs-4 .text-blue-100 }

Calculates if an axis-bound cylinder is within an AABB world-positioned box   
Returns `result: bool`, `mag-normal: Vector`, `hit: Vector` 
- Hit vector will be the closet point in the box to the cylinder origin     
- Origin starts the bottom of the cylinder, easier

### lib.IntersectSphereWithAABB
{: .d-inline-block }
(org: Vector, radius: float, boxmin: Vector, boxmax: Vector)
{: .d-inline .fs-4 .text-blue-100 }

Calculates if a sphere is within an AABB world-positioned box   
Hit vector will be the closet point in the box to the sphere origin    
Returns `result: bool`, `mag-normal: Vector`, `hit: Vector`   
 
### lib.IntersectABCylinderWithOBB
{: .d-inline-block }
(cylOrg: Vector, cylRadius: float, cylHeight: float, boxorg: Vector, boxangle: Angle, boxmin: Vector, boxmax: Vector)
{: .d-inline .fs-4 .text-blue-100 }

### lib.IntersectSphereWithOBB
### lib.PlaneToNormal
### lib.InsideOutTest

## Utility
### lib.RectToMeshEx