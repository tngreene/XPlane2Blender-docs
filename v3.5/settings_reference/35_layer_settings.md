# Layer Settings
During the export process, Blender data (meshes, animations, materials, etc) are combined with X-Plane Layers and turned into .OBJs. Depending on your export mode defined in the [scene settings](mkdownhere), the layer settings will appear in the Blender Properties Pane's Scene tab, or in selected root Object's Object's pane. All options are the same, regardless of export mode and where they appear in the UI. The only difference you may see is that in Layers mode, an X-Plane Layer settings section will have a header of Layer #, and in Root Objects mode will simply have the header of "Root Objects". This is purely cosmetic.

## Basic Settings
``Name`` - This is the name of the layer and ultimately the file name of the OBJ. When empty and in "Layers" export mode, the name "layer_x" is automatically applied, where x is the layer number. When empty and in "Root Object" export mode, the root object's name will become the layer name. If the name is a relative path, the exporter will automatically create the folders necessary.

``Type`` - The type of X-Plane OBJ being exporter. This greatly changes what options are available and the behavior of the exporter.
	- Aircraft (Part): For parts of an aircraft to be tied together with Plane Maker. Supports panel textures. The default choice
	- Cockpit: For parts of an airplane's cockpit. Shows Cockpit Regions options and hides LODs options. Cockpit objects also support panel textures
	- Scenery Object: Objects that are drawn as scenery. They can include draped geometry that hugs the ground
	- Instanced Scenery Object: Like a scenery object, but is instance-able. Instancing is the ability for X-Plane draw more than one OBJ in a single stroke with the GPU. The less complicated the OBJ, the more likely it will pass for being instance-able. A massive performance booster for your model

## Textures
X-Plane textures must be a .dds or .png file. Blender supports both. A .png will surfice for most applications. See [Texture Settings](./34_texture_settings.md) for more information.

``Autodetect Textures`` | On | Turns on or off autodetecting an OBJ's textures from Blender's material's texture slots. When unchecked, text fields will appear and you will be able to manually specify which textures should be used. **Beware: Some material and textures validations will be turned off!** In addition, Composite Normal-Textures will be ignored for this layer.|

Setting | Default | Description | Requirement(s)
------- | ------- | ----------- | --------
``Default`` | "" | The file path to the daytime texture to be used for this object |
``Night`` | "" | The file path to the night time texture to be used for this object|
``Normal``| "" | The file path to the normal/specular map to be used for this object | For more details about what types of textures can be used in this slot, see [more info here].
``Draped``| "" | The file path to the draped texture | Layer type must not be aircraft or Cockpit
``Draped Normal``| "" | The file path to the draped normal texture | Layer type must not be aircraft or Cockpit

Objs can still be exported, even if ``Autodetect Textures`` is turned off, and any of these file paths is left blank.

## Levels of Detail
Setting | Default | Description | Requirement(s)
------- | ------- | ----------- | --------
``LODs`` | "None" | Specifies the number of LOD bins to customize. When set to a number, that many sub LOD boxes will come up, allowing you to specify per bin. Each LOD bin has a ``Near`` and ``Far`` clipping distance (by default 0). The OBJ will only be visible at between those distances. When having 2 or more LODs, make sure they overlap or your model will flicker: (0,1000),(1000,3000),(3000,6000).
``Max. Draped LOD`` | 0.00 | Determines maximum LOD distance for draped geometry. 0 means "As far as possible."| ``Type`` must be "Scenery" or "Instanced Scenery".

## Scenery Properties
Perhaps a bit misnamed, this group is not entirely exclusive to just Scenery and Instanced Scenery Exports.

### Layer Grouping
Setting | Default | Description | Requirement(s)
------- | ------- | ----------- | --------
``Layer Group``|"None"|Layer groups are a way to influence the draw order of scenery. It can be done at large by "Group" or at a smaller scale per group via the ``Layer Group Offset``. The categories of each are (hopefully) self explanatory|
``Layer Group Offset``|0|A layer group offset attempts to fine tune the draw order for this OBJ within its layer group|
``Draped Layer Group``|"None"|Like ``Layer Group`` but for draped objects| Only available for "Scenery" and "Instanced Scenery" exports
``Draped Layer Group Offset``|0|Like ``Layer Group Offset`` but for draped objects| Only available for "Scenery" and "Instanced Scenery" exports

### Slope Properties
These settings change when and how a scenery object rests on the ground.

Setting | Default | Description | Requirement(s)
------- | ------- | ----------- | --------
``Slope Limit``|Off|Enables or disables an OBJ's slope limit, the minimum and maximum pitch and roll of a slope X-Plane can select the OBJ for. . Enabling ``Slope Limit`` opens additional options. See [here](http://developer.x-plane.com/?article=obj8-file-format-specification#SLOPE_LIMIT_ltmin_pitchgt_ltmax_pitchgt_ltmin_rollgt_ltmax_rollgt)|

Setting | Default | Description | Requirement(s)
------- | ------- | ----------- | --------
``Tilted``|Off| When checked, X-Plane rotates the object before placing square on the ground even when the ground is a slope, as opposed to placing as if it were flat relative to gravity|
``Required Surface``|"Any"|Requires X-Plane to place this OBJ on only certain kinds of surfaces: "Dry", such as land or "Wet", such as oceans, rivers, and lakes, or "Any" for either of them|

## Advanced Options

Setting | Default | Description | Requirement(s)
------- | ------- | ----------- | --------
``Particle System File`` | "" | A relative filepath to a particle system file. Emitters in the obj will reference names in this file | ``Export Version`` must be at least "11.30", file must end in .pss
``Slung-Load Weight`` | 0 | **A float indicating the weight in pounds the object is.** It is used by physic engine for things carried (and possibly dropped) by planes. |
``Export`` | On | **Determines whether or not the layer is exported.** Only useful to turn off when you want to debug a scenery object by not having it there. | 
``Debug`` | On | **Determines whether or not the layer will emit debug information if Scene's ``Debug`` is turned on**. Has no impact on OBJ performance. |

## Export Path Directives
Export Path Directives are unofficial OBJ directives that an internal Laminar Research tool uses to extract and automatically generate library.txt files from. EXPORT directives are ignored by X-Plane.

When the button ``Add Export Path Directive`` is pressed, a new Export Path directive slot is added. When the x-mark on the directive is clicked, it is removed. Empty export path directives are skipped.

## Custom Properties
Custom properties are a key value pair, which get written directly to the header of the OBJ file, completely without validation. Some use this for 3rd party plug-ins or tooling or to gain access to new OBJ features that are not yet built into the exporter. For the latter case, this is NOT recommended and should be deprecated as soon as the exporter supports the OBJ directive! Without rigorous, spec compliant, and tested validation OBJs could become invalid or slow.
