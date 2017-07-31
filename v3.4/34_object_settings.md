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


