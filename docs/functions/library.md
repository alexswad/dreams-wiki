---
title: General Library
layout: default
nav_order: 15
parent: Functions
---
Functions under Dreams.Lib.*
- TOC
{:toc}

## Traces
### Lib.TraceRayPhys
{: .d-inline-block }
(phys: DreamPhys, start: Vector, dir: Vector, distance)
{: .d-inline .fs-4 .text-blue-100 }
Completes a ray-trace aganist a DreamPhys table, usually \<Room\>.phys  
Returns `hit`, `fraction`, `normal`

## Intersections
### Lib.IntersectABCylinderWithAABB
{: .d-inline-block }
(cylOrg: Vector, cylRadius: float, cylHeight: float, boxmin: Vector, boxmax: Vector)
{: .d-inline .fs-4 .text-blue-100 }
Calculates if an axis-bound cylinder is within an AABB container   
Returns `result: bool`, `normal: Vector`, `penetration-dist: Vector`
- Origin starts the bottom of the cylinder, easier for player collisions

### Lib.IntersectSphereWithAABB
{: .d-inline-block }
(sphereOrg: Vector, radius: float, boxmin: Vector, boxmax: Vector)
{: .d-inline .fs-4 .text-blue-100 }

Calculates if a sphere is within an AABB container  
Returns `result: bool`, `normal: Vector`, `penetration-dist: Vector`   
 
### Lib.IntersectABCylinderWithOBB
{: .d-inline-block }
(cylOrg: Vector, cylRadius: float, cylHeight: float, boxorg: Vector, boxangle: Angle, boxmin: Vector, boxmax: Vector, sizex: int, sizey: int, sizez: int)
{: .d-inline .fs-4 .text-blue-100 }
Calculates if an axis-bound cylinder is within an OBB container
`sizex`, `sizey`, `sizez` are the Half-Extents of the OBB container
Returns `result: bool`, `normal: Vector`, `penetration-dist: Vector`   
- Origin starts the bottom of the cylinder, easier for player collisions

### Lib.IntersectSphereWithOBB
{: .d-inline-block }
(sphereOrg: Vector, radius: float, boxorg: Vector, boxangle: Angle, boxmin: Vector, boxmax: Vector)
{: .d-inline .fs-4 .text-blue-100 }
Calculates if a sphere is within an OBB container  
Returns `result: bool`, `normal: Vector`, `penetration-dist: Vector`   

## Vector Math
### Lib.PlaneToNormal
{: .d-inline-block }
(p1: Vector, p2: Vector, p3: Vector)
{: .d-inline .fs-4 .text-blue-100 }  
Returns `normal: Vector` from three points defining a plane

### Lib.InsideOutTest
{: .d-inline-block }
(p1: Vector, p2: Vector, p3: Vector, inside_point: Vector)
{: .d-inline .fs-4 .text-blue-100 }
Returns `result: bool` whether `inside_point` is on the same side as `p3` of the line defined by `p1` and `p2`    

### Lib.RotationMatrixFromNormals
{: .d-inline-block }
(normal1: Vector, normal2: Vector, normal3: Vector)
{: .d-inline .fs-4 .text-blue-100 }  
Returns a rotational `matrix: VMatrix` from three orthogonal normals


### Lib.MinMaxVecs
{: .d-inline-block }
(min, max, vector)
{: .d-inline .fs-4 .text-blue-100 }
Returns a new `min: Vector, max: Vector` set with `vector` included

### Lib.HalfExtentsFromBox
{: .d-inline-block }
(min, max)
{: .d-inline .fs-4 .text-blue-100 }
Returns a `table {1 = x, 2 = y, 3 = z}` with the half extents of each axes

### Lib.IsSquare
{: .d-inline-block }
(verts: table)
{: .d-inline .fs-4 .text-blue-100 }
Returns `result: bool` if a table of verts on a plane form a square

### Lib.MagnitudeToNormal
{: .d-inline-block }
(xdelta: float, ydelta: float, zdelta: float)
{: .d-inline .fs-4 .text-blue-100 }

Returns the `normal: Vector` facing the direction of the axis of the highest magnitude   
Used by Cylinder and Sphere intersections   
`delta` variables use their absolute value internally

### Lib.HighestMag
{: .d-inline-block }
(xdelta: float, ydelta: float, zdelta: float)
{: .d-inline .fs-4 .text-blue-100 }
forgot why I made this might be removed
{: .label .label-red }
Returns `string: x/y/z` corresponding to the axis with the highest magnitude

## Utility
### Lib.RectToMeshEx
{: .d-inline-block }
(l, w, h, origin: Vector, [ignore: table, reverse_faces: bool, utex_add, vtex_add])
{: .d-inline .fs-4 .text-blue-100 }
Creates a rectangle for rendering meshes, `origin` starts in the left corner