# Material Settings
XPlane2Blender's material model is different from Blenders. In XPlane2Blender, all Blender objects must have at least 1 material and only the first one is chosen for export. A material can have any number of material slots that do the majority of the work changing how it looks in X-Plane.

Due to some inconviences of Blender's data model, some UI elements will be shown even if using them would result in an invalid OBJ or not change the export at all.

## Relavent Blender Settings
### Specular
``Intensity`` - **A float from 0.00 to 1.00. All materials in an OBJ must have the same specularity.**

## XPlane2Blender Settings
### Draw Linked Objects
These settings are used to decide when and how to draw the material.

``Draw Linked Objects`` - **A checkbox that, if checked, draws any objects that uses the material. If unchecked, objects that use this material will not be drawn.**

``Draped`` - **A checkbox that, if checked, makes this a draped material that hugs the ground.** This is only valid for Scenery and Instance Scenery exports [mkdown link]

``Normal Metalness`` - **Requires version to be greater or equal to X-Plane 11. A checkbox that when checked tells X-Plane to take the blue channel of this material's normal map to be used as base reflectance.** This is commonly used for metal-like surfaces.

``Blend`` - **A drop down menu of "Blend Glass", "Shadow", "Alpha Cutoff", "Alpha Blend", "Alpha Blend" by default.** Blend mode controls how something or other does a thing.

- Blend Glass
- Blend Shadow
- Alpha Cutoff
- Alpha Blend

``Alpha Cutoff Ratio`` - **Requires Blend set to Alpha Cutoff. A float that goes from 0.0 to 1.00. Alpha levels in the texture below this level are rendered as fully transparent and alpha levels above this level are fully opaque",
        default = 0.5,**

### Surface Behavior
Surface Behavior settings control how this material interacts with X-Plane in ways besides how it looks.

``Surface Type`` - **A drop down menu of types of surfaces that X-Plane can simulate the bumpiness of. Grass is more bumpy that concrete, for instance.** If not specified a smooth surface is used. (Does this affect PBR?)

``Deck`` - **When ``Surface Type`` is not "None", this can be checked. It will allow you to move under the material.**

``Camera Collition`` - **When checked the X-Plane camera will collide with this and not be able to move through it.**

### Light Levels
``Override Light Level`` - **When checked, X-Plane's chosen object night lighting is overriden with custom dataref driven values.**
``Value 1`` - **First value to be mapped to the dataref**
``Value 2`` - **Second value to be mapped to the dataref**
``Dataref`` - **The dataref to change the value of the material's night time lighting level**

### Day-Night Preview Balance
This setting provides a convient way to preview the material in Blender's 3D View. To enable the Day-Night Preview feature, add an albedo texture (uses Diffuse->Color) and a night texture (uses Shading->Emit)"

``Day-Night Preview Balance`` - If you have a daytime and night time texture [see auto detecting textures](mkdown), sliding this will automatically adjust their preview in the 3D Viewer. It does not change exported OBJs. Default .5

### Instancing Effects
These settings can only apply to ``Instance Scenery`` exports.

``Tint`` - **If checked, Albedo Tint and Emissive Tint settings will be enabled.**
``Albedo`` - **A float between 0.0 and 1.0, where 0.0 is no darkening of the albedo (day time) texture and 1.0 is total darkening of the albedo texture."**
``Emmisive`` - **A float between 0.0 and 1.0, where 0.0 is no darkening of the emmisve (day time) texture and 1.0 is total darkening of the emmisive texture."**

### Polygon Offset
``Polygon Offset`` - **An int that indicates to X-Plane what order the object should attempt to be drawn in, from farthest away from the player camera to closets. 0 by default, meaning let X-Plane make all the decisions.** Very useful for an object with many parts that are close together. See the blog post [The road to hell is paved with ATTR_poly_os](http://developer.x-plane.com/2006/09/the-road-to-hell-is-paved-with-attr_poly_os/) for a more detail.

### Cockpit Panel
``Part Of Cockpit Panel`` - **If check, objects will this material will use the panel texture and will be clickable.**

``Cockpit Region`` - **Defines which, region this material should appear in. If set to none, no region will be used. The region number refers to the regions defined in X-Plane Layer's Cockpit Regions.**

### Custom Properties
See Object materials
