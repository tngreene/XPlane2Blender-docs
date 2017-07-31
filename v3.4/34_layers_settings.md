# Layers Settings
During the export process, Blender data (meshes, animations, materials, etc) are combined with X-Plane Layers and turned into .OBJs. Depending on your export mode defined in the [scene settings](mkdownhere), the layer settings will appear in the Blender Properties Pane's Scene tab, or in selected root Object's Object's pane. All options are the same, regardless of export mode and where they appear in the UI. The only difference you may see is that in Layers mode, an X-Plane Layer settings section will have a header of Layer #, and in Root Objects mode will simply have the header of "Root Objects". This is purely cosmetic.

## Basic Settings

``Name`` - **A textfield, empty by default. .obj file name is layer_x where x is the layer number during layers mode or the name of the root object during Root Object mode if left blank.** This is the name of the layer, and ultimately the file name of the .obj. Clever users can specify file paths relative to the blend file in the name and have the exporter automatically place things into groups. For instance, 'landing/left_wheel' is a valid name and would automatically create the folder "landing" in the same directory as the save target. ".obj" is automatically appended as needed. 

``Type`` - **A drop down menu of "Aircraft (Part)","Cockpit","Scenery Object", and "Instanced Scenery Object". "Aircraft (Part)" by default** The type of X-Plane OBJ being exported. This greatly changes what options are available and the behavior of the exporter.
	- Aircraft (Part): For parts of an aircraft to be tied together with Plane Maker. Supports panel textures.(insert markdown)
	- Cockpit: For parts of an airplane's cockpit. Shows Cockpit Regions options and hides LODs options. Cockpit objects also support panel textures.
	- Scenery Object: Objects that are drawn as scenery. They can include draped geomerty that hugs the ground
	- Instanced Scenery Object: Like a scenery object, but is instance-able. Instancing is the ability for X-Plane draw more than one OBJ in a single stroke with the GPU. The less complicated the OBJ, the more likely it will pass for being instance-able. A massive preformance booster for your model.

## Textures

``Autodetect Textures`` - **A checkbox which turns on or off autodetecting textures from Blender's material's texture slots. On by default.** The autodetection algorithm is detailed [here]. When unchecked, text fields will appear and you will be able to manually specify which textures should be used. **Beware: some material and textures validations will be turned off!** In addition, Composite Normal-Textures will be ignored for this layer.

## Levels of Detail
``LODs`` - **A drop down of "none","1","2","3","4". "none" by default." Specifies the number of LOD bins to customize.** When set to a number, that many sub LOD boxes will come up, allowing you to specify per bin. Each LOD bin has a ``Near`` and ``Far`` clipping distance (by default 0). The OBJ will only be visible at between those distances. When having 2 or more LODs, make sure they over lap or your model will flicker: (0,1000),(1000,3000),(3000,6000).

``Max. Draped LOD`` - **A float which determines maximum LOD distance for draped geometry. 0 meaning as far as possible. 0 by default. Only avaiable for Scenery and Instanced Scenery export.**

## Scenery Properties

Perhaps a bit misnamed, this group is not entirely exclusive to just Scenery and Instanced Scenery Exports.

### Layer Grouping
``Layer Group`` - **A drop down menu of X-Plane Layer Groups, by default "None".** Layer groups are a way to influence (but not control) the draw order of scenery. It can be done at large by "Group" or at a smaller scale per group via the ``Layer Group Offset``.

	The full list of (self explanitory) layer groups:
	- "None"
	- "Terrain"
	- "Beaches"
	- "Shoulders"
	- "Taxiways"
	- "Runways"
	- "Markings"
	- "Airports"
	- "Roads"
	- "Objects"
	- "Light Objects"
	- "Cars"

``Layer Group Offset`` - **An integer to attempt to fine tune the number within that layer group. 0 by default.**

``Draped Layer Group`` - **Like ``Layer Group`` but for draped objects. Only available for Scenery and Instanced Scenery exports.**

``Draped Layer Group Offset`` - **Like ``Layer Group Offset`` but for draped objects. Only available for Scenery and Instanced Scenery exports.**

### Shadows
Most shadow properties are set in the material settings, except for ``Cast Shadow (Global)``.

``Cast Shadow (Global)`` - **A checkbox which controls if the exported OBJ will cast any shadows what so ever. On by default.** If unchecked, the OBJ will never cast shadows.

### Slope Properties
These settings change when and how a scenery object rests on the ground.

``Slope Limit`` - **A checkbox which enables or disables an OBJ's slope limit. Off by default. Turning it on opens additional options to specify a minimum and maximum pitch and roll.** An obj's slope limit dictates the minimum and maximum pitch and roll of a slope X-Plane can select it for. See [here](http://developer.x-plane.com/?article=obj8-file-format-specification#SLOPE_LIMIT_ltmin_pitchgt_ltmax_pitchgt_ltmin_rollgt_ltmax_rollgt)

``Tilted`` - **A checkbox which, when turned on, makes X-Plane rotate the object before placing square on the  ground even when the ground is a slope, as opposed to placing as if it were flatit relative to gravity. Off by default.**

``Required Surface`` - **A drop down menu of surfaces types containing "Wet", "Dry", and "Any". Default "Any".** Requires the surface for the OBJ to be placed on to be a certain kind.

## Advanced Options

``Slung-Load Weight`` - **A float indicating the weight in pounds the object is. 0 by default.** It is used by physic engine for things carried (and possibly dropped) by planes. 

``Export`` - **A checkbox which determines whether or not the layer is exported. On by default.** Only useful to turn off when you want to debug a scenery object by not having it there.

``Debug`` - **A checkbox which determines whether or not the layer will emmit debug informaiton. On by default.** The debug information will only show up if the Scene Setttings' [mkdownlink] ``Debug`` is also on. Turning this off will have no affect on OBJ preformance.

Remove checkbox from everything

