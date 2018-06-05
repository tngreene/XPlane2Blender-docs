# Animation Requirements For Smart Manipulators

Manipulators lets you specify how objects in Blender become interactive in X-Plane. In X-Plane 11.1x, you can now specify new manipulators which give a better experience in virtual reality. These new VR manipulators are

Manip Type | Potential Uses
-----------|--------------
``Drag Axis``*               | Flap handles, parking brakes, simple air vents, or anything that move sin a linear fashion
``Drag Axis With Detents``   | Any Drag Axis application, but with detents to overcome
``Drag Rotate``              | Throttle quadrants, trim wheels, cowl flaps. Any mechanism that rotates around a fixed point
``Drag Rotate With Detents`` | Any Drag Rotate application, but with detents to overcome

These manipulators use animation data to autodetect properties such as ``X``, ``Y``, ``Z``, ``v1 Min/Max``, etc. Dataref 1 and 2 can always be overridden manually. This article describes in detail the requirements for each.

*Drag Axis is an old manipulator now upgraded. Use the ``Autodetect Settings`` checkbox to opt in.

## Further Reading
Manual Pages
[Object Settings](../../v3.4/settings_reference/34_object_settings.md)

Manipulators
- [Manipulators In-depth](../../v3.4/indepth/manipulator_recipes.md)
- [Manipulators](https://developer.x-plane.com/?article=manipulators)

VR
- [Manipulators and VR Part 1: From Mouse to Mechanism](https://developer.x-plane.com/2018/01/manipulators-and-vr-part-1-from-mouse-to-mechanism/)

Example Blend Files
- [example_vr_manipulator_types.zip](./content/example_vr_manipulator_types.zip)
This zip of blend files contains a variety of examples of working and not working smart manipulators, taken from the XPlane2Blender test suite. Don't get the wrong idea, these are only some (simple) use cases of the feature.

## About "Animation Sources"
The autodetection algorithm requires a certain number of animation sources, of certain types, in a certain order. The algorithm continues looking for animation sources until it fills its requirements, starting at the manipulator's mesh and then inspecting up its parents. This provides flexibility. Animations can appear anywhere in this chain from, including having gaps between and not having the manipulator mesh be the first animation source.

The ...-> indicates 0 or more non-animated meshes or bones are allowed in between.

Type | Animation Requirements (Listed In Expected Order)
-----|--------------------------------------------------
Drag Axis                | [Manipulator Mesh]...->Location Animation
Drag Axis With Detents   | [Manipulator Mesh]...->Location (Detent) Animation...->Location Animation
Drag Rotate              | [Manipulator Mesh]...->Rotation Animation
Drag Rotate With Detents | [Manipulator Mesh]...->Location (Detent) Animation...->Rotation Animation

## Animation Source Rules
### Common Animation Rules
- Must have one and only one dataref animation
- Must have actual movement (no animations of 0 degrees of rotation or 0 meters of movement)
- The mesh the manipulator is attached to must not have child datablocks or bones

### Location Animation Rules
- Must have exactly two non-clamping Location keyframes and **no** Rotation keyframes

### Rotate Animation Rules
- Must have exactly two non-clamping Rotation keyframes and **no** Location keyframes
- Must rotate around only one axis of rotation (in any rotation mode)
- Dataref keyframe values must be in ascending or descending order

### Detent Location Animation Rules
Drag Axis With Detents:
- Must have a parent with a valid location animation source
- The detent axis must be at 90 degrees from the drag axis

Drag Rotate With Detents:
- Must have a parent with a valid location animation source
- The detent axis must not be along the rotational axis in any way. To understand why, imagine a wheel that has been welded onto an axle. The axle is along the X axis, therefore the wheel rotates around the X axis. When X-Plane simulates how a mouse drag or VR drag rotates this object, it only calculates how the wheel could possibly move. Therefore any dragging along the X axis is ignored and no detenting in that direction is possible
- Must have exactly two non-clamping Location keyframes and **no** Rotation keyframes
- Must have [Axis Detent Ranges](./axis_detent_range.md)

### Drag Rotate Regions
By adding additional keyframes between the start and end of a ``Drag Rotate`` or ``Drag Rotate With Detents``' rotation, X-Plane will automatically adjust how long it takes to drag through those areas. In general, a large range will be slower to drag through, and a small range will be faster to drag through.

Keyframe # | Degrees | User Experience While Dragging At Constant Speed
---|-----------|-------------------------------------------------
1  | 0 - 90    | Manipulator will rotate **slowly** through this section 
2  | 90 - 150  | Manipulator will rotate **quickly** through this section 
3  | 150 - 180 | Manipulator will rotate **the quickest** through this section 

The speed is also affected by the ratio between degrees and size of dataref change.

Clamping is supported and recommended.

