# Object Settings
A Blender object's settings are accessed via the X-Plane panel under the Properties Pane's "Object" tab. Each Blender object has it's settings are set per object. Object settings are available for mesh, empty, armature, and lamp data-blocks.

## Relevant X-Plane Settings
Blender Object's Transformation and Relation data can be important to exporting OBJs.

### Transform
Setting | Description | Can Keyframe Values?
------- |  ----------- | --------
``Location``| The X, Y, Z co-ordinates of the object, relative to its parent or the world origin. Changing these values change where the model is located in X-Plane|Yes
``Rotation``| The degrees of rotation around the X, Y, Z (axis-angle and Quaternion also have a W) axis of rotation the object, relative to its parent or the world origin. Changing these values change where the model is rotated in X-Plane|Yes
``Scale``| The scaling factor of the model along it's X, Y, Z axis| No, the change to the object's vertices due to scaling is only saved to the OBJ once

``Rotation Mode`` - The rotation mode for Blender rotations. XPlane2Blender supports all modes and exports them equally

### Relations
``Layers`` - An array of true/false toggle switches that correspond to what Blender layers it is in. When ``Export Mode`` is set to "Layers Mode", this changes which X-Plane layer (and therefore OBJ) the object gets collected and placed into. In "Root Object" mode it has no affect on the output or execution of the exporter

## XPlane2Blender Settings

## Root Object
 ``Root Object`` - Off by default. When ``Export Mode`` is set to "Root Object" this checkbox will appear. Checking it will set this to be a ``Root Object``. Settings to control the X-Plane layer this and child objects will be collected into will appear underneath. These are the exact same settings used in Layers Mode and found under the "Scene" tab.

### Datarefs
Blender's location and rotation keyframes export where the geometry of objects should be in an animation, dataref keyframes describe how X-Plane should play the animation. This is different from traditional animation, where the animation tells a rendering engine (such as a 3D movie exporter) how to move geometry over time. Based on the value of a dataref inside X-Plane, X-Plane's rendering engine will interpolate between keyframes and display your model at specified positions.

For instance, to animate a yoke moving forward and back based on a player's joystick, you would use the dataref "sim/joystick/yoke_pitch_ratio". In X-Plane, this dataref will have a value between -1.00 and 1.00 (inclusive). In Blender you would model the yoke (the geometry), and create at least 2 Blender location and rotation keyframes, say, all the way forward on frame 1 and all the back on frame 2. You would then create X-Plane dataref keyframes on frame 1 and frame 2, with a value of -1.00 and 1.00 respectively. In sim, if the dataref is 0, X-Plane will automatically figure out how to position and rotate the yoke halfway between the position specified at frame 1 and the position specified at frame 2 (aka half way). If the dataref is -.80, X-Plane will automatically position the yoke almost all the way towards the position specified at frame 1 (almost all the way forward).

The more frames you add in Blender, the more precisely you can control the animation. Suppose the yoke in your aircraft has a dead-zone near the half way point. By specifying additional frames to show a slow down and specifying at what value of "sim/joystick/yoke_pitch_ratio" the player should see that frame, you can produce complex animations!

Since Blender's frames per second based timeline and X-Plane's dataref based "timeline" are different, you can use Blender's animation tools to preview but not directly export animations.

#### Dataref Animation Details 
Use ``Add Dataref`` to add a dataref animation section, and click the small white ``X`` in the top right corner of a dataref animation section to remove it.

``Dataref Path`` - Empty by default, this is the dataref for this animation. The dataref must be a standard X-Plane dataref or one supported by a plugin. It is not validated by XPlane2Blender.

``Search datarefs`` - When clicked, the default web browser will open the site https://www.siminnovations.com/xplane/dataref/index.php where one can search for applicable datarefs. www.siminnovations.com is a third-party website not supported by Laminar Research. It is provided as a convenience only and is not guaranteed to be up to date or correct.

``Animation Type`` - The type of animation to export. The types X-Plane supports are "Show", "Hide", and "Transform" (the default).

- "Show"/"Hide" animations show or hide the object when a dataref is greater than or equal to ``Value 1`` and less than or equal to ``Value 2``. Blender keyframes are not needed to enable show hiding animations. Since the range between Value 1 and 2 is inclusive, both a show and hide animation are necessary.

	For example, suppose you have a dataref that is between 0 and 1 and you want to create an object that is shown between 0 and 1 and hidden after that. One would select that object, create a "Show" dataref animation with Value 1 as 0 and Value 2 as 1, and a "Hide" animation with Value 1 as 1 and Value 2 being 1 or higher.

- "Transform" animations use Blender location and/or rotation keyframes to transform objects in space. Thusly, Blender animation keyframes on the selected object or armature are required before the following options are shown.

#### Transform Dataref Animations
Each frame on Blender's timeline is a place to add or remove a dataref keyframe. 

``Add/Update an X-Plane Keyframe`` and ``Remove an X-Plane Keyframe`` - Each button, with the icon of a key and key with a red slash through it, add/update or remove X-Plane Dataref keyframes to an object. These keyframes are combined with the Blender's keyframes and exported as animation inside the OBJ.

``Value`` - When the dataref is this value, X-Plane will have interpolated the animation to this frame. It is 0 by default, but that does not mean that is a valid number for all datarefs. You must look up documentation for each dataref and see which datatype are range of numbers it requires. Every time you change the value, you must also click the ``Add/Update an X-Plane Keyframe`` button before switching frames. Otherwise the value will not get saved.

``Animation Loops Every`` - Looping allows you to create an animation that repeats, even when the dataref driving the animation is not a fixed set of values. One could think of it as "when the dataref has advanced by this much, loop the animation back to the beginning". Only one loop value is allowed per animation, on the last keyframe in an animation or shortly thereafter.

If a dataref possible values are unbounded (increases infinitely) instead of in a range or set of values, it is still possible to get a repeating animation. When looping is not 0.00, use looping to still get repeating animation. , instead of **A float, incrementing by, .03, describing the amount of loops the animation will preform. 0.00 by default, making for 0% looping.** See [whatever] for more details.

#### Show/Hide Animations
Show/Hide has two values, where the object will be shown/hidden when the data is greater than or equal to ``Value 1`` and less than or equal to ``Value 2``. Datarefs that conflict about showing and hiding are not validated by the exporter.

#### Export Animation In Layers
```Export Animation In Layers`` - **An array of checkboxes, mirroring Blender's Object Layer visibility, all enabled by default. Only available in [Layers Mode](mkdown).** If a layer checkbox is disabled, then only the Blender Object's mesh will be exported in the layer, but **not** any of it's animations.

### Manipulator Settings

Manipulators are part of the cockpit objects. They let you assiagn ways to use inputs to control the object. The following are availible after ``Manipulator`` is checked.

Depending on type, different options are available to set for the manipulator. See the Manipulator spec [here](http://developer.x-plane.com/?article=manipulators#Types_of_Manipulators)

#### Types Of Manipulators

##### None
The default, clicking on an object does nothing. Non-cockpit objects always have no manipulator.

##### Panel Click
Includes 
	- 
``Requires object with panel texture or panel texture region.`` A click on the object is mapped through to the 2-D panel based on the panel texture's mapping.

##### Drag-Axis

##### 2-d Drag

##### Command
##### Command-Axis
##### Opaque
This sets the manipulation to 'no-op' (no operation). Unlike "none" manipulation, opaque manipulation "swallows" the mouse, preventing it from clicking on other manipulators that may lie behind it. It would typically be used to act as a safety-guard over a switch.

Each Manipulator type will allow you to set one or more of the following.

#### Drag

#### Manipulator Values

Different manipulators will have you set different values to fill out. Rather than listing every possible combination, here is what each means individually. Each value type has the same meaning, regardless of ``Manipulator Type`` chosen.

If a value is connected to a dataref
 
##### Common Manipulator Values
- ``Drag X`` - Length of X axis (meters)
- ``Drag Y`` - Length of Y axis (meters)
- ``Drag Z`` - Length of Z axis (meters)
- ``Value 1`` - Value 1 of the range of values over which a Drag Axis manipulator changes it's dataref
- ``Value 2`` - Value 2 or the range of values over which a Drag Axis manipulator changes it's dataref
- ``Value 1 Min`` - Minimum for a 2D Drag manipulator's dataref 1 range (-x to +x)
- ``Value 1 Max`` - Maximum for a 2D Drag manipulator's dataref 1 range (-x to +x)
- ``Value 2 Min`` - Minimum for a 2D Drag manipulator's dataref 2 range (-y to +y)
- ``Value 2 Max`` - Maximum for a 2D Drag manipulator's dataref 2 range (-y to +y)
- ``On Value`` - On value for toggle (must match value of dataref)
- ``Off Value`` - Off value for toggle (must match value of dataref)
 
##### Command Manipulator Values
- ``Command`` - The command to fire when manipulator is used
- ``Positive Command`` - Command to be executed when cursor is in positive region of Command Axis manipulator and mouse is being held down
- ``Negative Command`` - Command to be executed when cursor is in negative region of Command Axis manipulator and mouse is being held down
 
- ``Dataref 1`` - The first dataref to be modified by the manipulator
- ``Dataref 2`` - The second dataref to be modified by the manipulator
 
- ``Step`` - Dataref increment
 
##### Mouse Manipulator Values
- ``Value On Mouse Down`` - Value to set dataref on mouse down
- ``Value On Mouse Up`` - Value to set dataref on mouse up
- ``Value On Mouse Hold`` - Value to set dataref on mouse hold
- ``Click Step`` - Value change on click
- ``Hold Step`` - Value change on hold
- ``Wheel Delta`` - Value change on mouse wheel tick
- ``Exp`` - Power of an exponential curve that controls the speed at which the dataref changes. Higher numbers cause a more “non-linear” response, where small drags are very precise and large drags are very fast

#### LODs
``LODs`` - **Four checkboxes that determine which levels of detail X-Plane should place this object. By default all boxes empty, meaning place in every LOD catagory** LOD ranges are defined in the [layer](mk) settings.

#### Override Weight
``Weight`` - **An int used to offset the order in which similar elements are written to the Obj, by default 0.** Needs better desc.

#### Custom Object Properties
Objects can have custom properties (another name for attribute) as well. These will get written directly to the OBJ in the form of 

``Name`` - The name of the custom property
``Value`` - The value of the property
``Reset`` - OBJ attributes often come in pairs, such as ``ATTR_light_level`` and ``ATTR_no_light_level``. An attribute may be turned on at the beginning of an object in an OBJ, and turned off (aka reset) in time for the next one. In the case of ATTR_whatever, if it was never turned off every object afterward would take on that attribute. The value for ``Reset`` will be written before the next object starts.
``Weight`` - An int. The larger the weight the later it gets written in the OBJ

#### Custom Animation Properties
Objects can also have custom animation properties. These also get written directly to the OBJ in the form of ``Name Value`` with no validation.

``Name`` - **The custom animation directive to be written out. ANIM_ is *not* prepended**
``Value`` - **The value for the custom animation direcitve.**
``Weight`` - **An int. Attempts to change the order of the properties, with larger numbers written later.**

#### Object Conditionalization
Objects X-Plane 10 supports the conditionalization of OBJ files.  Conditionalization is a process whereby the contents of a file are skipped or used depending on rendering settings.  Typical uses of conditionalization are to change the appearance of an object when shadows are enabled, or when HDR is on.

``Variable`` - **A dropdown menu of "Global Shadows","HDR", and "Version 10x", "Global Shadows".**
``Must Be On`` - **A checkbox which, when checked, tells X-Plane this rendering variable must be on to draw the variable. If unchecked, it tells X-Plane this rendering variable must be off to draw the variable. Removing the conditional lets X-Plane make its own decisions.**
