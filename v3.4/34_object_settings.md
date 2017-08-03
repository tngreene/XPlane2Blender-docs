# Object Settings
Object Settings are accessed via the X-Plane panel under the Properties Pane's Object Tab. Object settings are set per object. Aside from ``Root Object`` being available when in Root Objects mode.

## Datarefs
Datarefs tie Blender Animations and [X-Player Layers](mkdownlink) together to export animations into OBJs. Blender's Location and Rotation keyframes provide the data for the motion, X-Plane's Dataref Keyframes provide the timing. This is different from the standard model of 3D Animation, where the animation tool not only provides geometry, keyframes, but also timing via the time line. X-Plane's internal clock provides the time, and stretches the animation between keyframes with its own animation engine. You just provide the 3D model and keyframes.

``Path`` - **A textfield which represents the dataref itself. Empty by default.** The path must be a valid dataref: either a standard X-Plane dataref or one supported by a plugin. It is not validated by XPlane2Blender.

``Search datarefs`` - **A button that, when clicked, will open the default web browser to the site [https://www.siminnovations.com/xplane/dataref/index.php](https://www.siminnovations.com/xplane/dataref/index.php) where one can search for applicable datarefs.** siminnovatoins.com is a third-party website not supported by Laminar Research. It is provided as a convience only and is not garunteed to be correct.

``Animation Type`` - **A drop down menu of ``Show``,``Hide``, and ``Transform``. ``Transform`` by default.** Show/hide animations will show/hide animations the model during the set keyframes. Transform makes the exporter take the object's translate and rotate properties and turn them into keyframes. Certain optimzations are preformed as possible. There is no scale option because scaling cannot be keyframed in X-Planed, only statically applied to the verticies of a model once. See [animations](mkdown)

If there is any animation data for this object or amatrue, the following options will appear:

### Transform Animations
Each frame on Blender's timeline is a place to add or remove an X-Plane Keyframe. 
``Add/Update Keyframe Button`` and ``Remove Keyframe Button`` - Each button, with the icon of a key and key with a red slash through it, add and remove X-Plane Dataref keyframes to an object. These key frames are combined with the Blender's keyframes and exported as animation inside the OBJ.

``Value`` - **The value of the dataref for X-Plane to keyframe to and interpolate with (fix that). 0 by default**. You must look up the documentation for each dataref. Some will only accept an integer, others will only accept a float between -1 and 1. This is not validated by XPlane2Blender. Every time you change the value, you must also click the Add Keyframe button.

``Loops`` - **A float, incrementing by, .03, describing the amount of loops the animation will preform. 0.00 by default, making for 0% looping.** See [whatever] for more details.

### Show/Hide Animations
Show/Hide has two values, where the object will be shown/hidden when the data is greater than or equal to ``Value 1`` and less than or equal to ``Value 2``. Datarefs that conflict about showing and hiding are not validated by the exporter.

### Export Animation In Layers
```Export Animation In Layers`` - **An array of checkboxes, mirroring Blender's Object Layer visibility, all enabled by default. Only available in [Layers Mode](mkdown).** If a layer checkbox is disabled, then only the Blender Object's mesh will be exported in the layer, but **not** any of it's animations.

## Manipulator Settings

Manipulators are part of the cockpit objects. They let you assiagn ways to use inputs to control the object. The following are availible after ``Manipulator`` is checked.

Depending on type, different options are available to set for the manipulator. See the Manipulator spec [here](http://developer.x-plane.com/?article=manipulators#Types_of_Manipulators)

### Types Of Manipulators

#### None
The default, clicking on an object does nothing. Non-cockpit objects always have no manipulator.

#### Panel Click
Includes 
	- 
``Requires object with panel texture or panel texture region.`` A click on the object is mapped through to the 2-D panel based on the panel texture's mapping.

#### Drag-Axis

#### 2-d Drag

#### Command
#### Command-Axis
#### Opaque
This sets the manipulation to 'no-op' (no operation). Unlike "none" manipulation, opaque manipulation "swallows" the mouse, preventing it from clicking on other manipulators that may lie behind it. It would typically be used to act as a safety-guard over a switch.

Each Manipulator type will allow you to set one or more of the following.

### Drag

### Manipulator Values

Different manipulators will have you set different values to fill out. Rather than listing every possible combination, here is what each means individually. Each value type has the same meaning, regardless of ``Manipulator Type`` chosen.

If a value is connected to a dataref
 
#### Common Manipulator Values
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
 
#### Command Manipulator Values
- ``Command`` - The command to fire when manipulator is used
- ``Positive Command`` - Command to be executed when cursor is in positive region of Command Axis manipulator and mouse is being held down
- ``Negative Command`` - Command to be executed when cursor is in negative region of Command Axis manipulator and mouse is being held down
 
- ``Dataref 1`` - The first dataref to be modified by the manipulator
- ``Dataref 2`` - The second dataref to be modified by the manipulator
 
- ``Step`` - Dataref increment
 
#### Mouse Manipulator Values
- ``Value On Mouse Down`` - Value to set dataref on mouse down
- ``Value On Mouse Up`` - Value to set dataref on mouse up
- ``Value On Mouse Hold`` - Value to set dataref on mouse hold
- ``Click Step`` - Value change on click
- ``Hold Step`` - Value change on hold
- ``Wheel Delta`` - Value change on mouse wheel tick
- ``Exp`` - Power of an exponential curve that controls the speed at which the dataref changes. Higher numbers cause a more “non-linear” response, where small drags are very precise and large drags are very fast

### LODs
``LODs`` - **Four checkboxes that determine which levels of detail X-Plane should place this object. By default all boxes empty, meaning place in every LOD catagory** LOD ranges are defined in the [layer](mk) settings.

### Override Weight
``Weight`` - **An int used to offset the order in which similar elements are written to the Obj, by default 0.**

### Custom Object Properties
Objects can have custom properties (another name for attribute) as well. These will get written directly to the OBJ in the form of 

``Name`` - The name of the custom property
``Value`` - The value of the property
``Reset`` - OBJ attributes often come in pairs, such as ``ATTR_light_level`` and ``ATTR_no_light_level``. An attribute may be turned on at the beginning of an object in an OBJ, and turned off (aka reset) in time for the next one. In the case of ATTR_whatever, if it was never turned off every object afterward would take on that attribute. The value for ``Reset`` will be written before the next object starts.
``Weight`` - An int. The larger the weight the later it gets written in the OBJ

### Custom Animation Properties
Objects can also have custom animation properties. These also get written directly to the OBJ in the form of ``Name Value`` with no validation.

``Name`` - **The custom animation directive to be written out. ANIM_ is *not* prepended**
``Value`` - **The value for the custom animation direcitve.**
``Weight`` - **An int. Attempts to change the order of the properties, with larger numbers written later.**

### Object Conditionalization
Objects X-Plane 10 supports the conditionalization of OBJ files.  Conditionalization is a process whereby the contents of a file are skipped or used depending on rendering settings.  Typical uses of conditionalization are to change the appearance of an object when shadows are enabled, or when HDR is on.

``Variable`` - **A dropdown menu of "Global Shadows","HDR", and "Version 10x", "Global Shadows".**
``Must Be On`` - **A checkbox which, when checked, tells X-Plane this rendering variable must be on to draw the variable. If unchecked, it tells X-Plane this rendering variable must be off to draw the variable. Removing the conditional lets X-Plane make its own decisions.**
