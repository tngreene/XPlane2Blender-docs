# Material Settings
XPlane2Blender's material model is different from Blender's. In XPlane2Blender, all Blender objects must have a material. If you have multiple materials, only the first one is chosen. A material can have any number of texture slots that do the majority of the work changing how an OBJ looks in X-Plane.

Due to some inconveniences of Blender's data model, some UI elements will be shown even if using them would result in an invalid OBJ or would have no affect.


## Relevant Blender Settings
### Link
``Link`` - The data-model linkage of the material **must be set to "Data"**. If you have materials that are linked by "Object", it is recommended to remove them to keep things neat

### Specular
Setting | Default | Description | Requirement(s)
------- | ------- | ----------- | --------
``Intensity``| 0.50 |How intense (bright) the specular reflection of the material is. All materials in an OBJ must have the same specularity|

## XPlane2Blender Settings
To get certain performance boosts or to have a valid export, some settings (such as Blend Glass and Normal Metalness) must be

Setting | Default | Description | Requirement(s)
------- | ------- | ----------- | --------
``Draw Objects With This Material`` | Off | If checked, any object that uses this material will be drawn. If left unchecked, any object that uses this material will not be drawn |
``Draped`` | Off | If checked, geometry with this material will hug the ground | Only valid for "Scenery" and "Instance Scenery" exports|
``Normal Metalness`` | Off | When checked, X-Plane will take the blue channel of this material's normal map and use it as base reflectance. This is commonly used for metal-like surfaces | ``Export Version`` must be greater or equal to "11.0x"
``Blend`` |"Alpha Blend"|Controls how texture's alpha channels are blended with each other. See the **Blend Mode Options Table** for more details| 
``Alpha Cutoff Ratio`` | 0.5 | For this material's textures, alpha levels below the ``Alpha Cutoff Ratio`` are rendered as fully transparent. Alpha levels above the level are fully opaque. Values can range from 0.00 to 1.00 | ``Blend`` must be set to "Alpha Cutoff"

### Blend Mode Options
Blend Mode | Description | Requirement(s)
---------- | ----------- | --------
"Blend Shadow"|In shadow mode, shadows are not blended but primary drawing is|
"Alpha Cutoff"|Textures alpha channel will be used to cutoff areas above the Alpha Cutoff Ratio|
"Alpha Blend"|Textures alpha channel will blended|

### Blend Glass
The alpha channel of the albedo (day texture) will be used to create translucent rendering. ``Export Version`` must be at least "11.0x"

### Cast Shadows (Local)

Setting | Default | Description | Requires
------- | ------- | ----------- | --------
``Cast Shadows (Local)`` | True | Controls whether the mesh with this material will cast shadows | X-Plane Version must be >= "10.10"

### Surface Behavior
Surface Behavior settings control how this material interacts with X-Plane in non-visual ways.

Setting | Default | Description | Requires
------- | ------- | ----------- | --------
``Surface Type``|"None" - a smooth surface | A drop down menu of types of surfaces that X-Plane can simulate the bumpiness of. Grass is more bumpy that concrete, for instance.|
``Deck``|Off| When checked, objects with this material can be flown or moved under|``Surface Type`` must not be "None"
``Camera Collision``|Off| When checked, the X-Plane camera will be prevented from moving through objects with this material| Always shown in UI but will only affect Cockpit objects

### Light Levels
Setting | Default | Description | Requires
------- | ------- | ----------- | --------
``Override Light Level``|Off|When checked, X-Plane's chosen object night lighting is overridden with custom dataref driven values|
``Value 1``|0.00|First value to be mapped to the dataref | ``Override Light Level`` is on
``Value 2``|0.00|Second value to be mapped to the dataref | ``Override Light Level`` is on
``Dataref``||The dataref to change the value of the material's night time lighting level | ``Override Light Level`` is on

### Day-Night Preview Balance
``Day-Night Preview Balance`` - This setting provides a convenient way to preview the material in Blender's 3D View. To enable the Day-Night Preview feature, add an albedo texture (uses Diffuse->Color) and a night texture (uses Shading->Emit) to the material. Adjusting this slider sliding this will automatically adjust their preview in the 3D Viewer. It does not change the content of exported OBJs.

### Instancing Effects
These settings can only apply to ``Instance Scenery`` exports.

Setting | Default | Description | Requirement(s)
------- | ------- | ----------- | --------
``Tint`` | Off | If checked, Albedo Tint and Emissive Tint settings will be enabled. |
``Albedo`` | 0.0 | A float between 0.0 and 1.0, where 0.0 is no darkening of the albedo (day time) texture and 1.0 is total darkening of the albedo texture|
``Emissive`` | 0.0 | A float between 0.0 and 1.0, where 0.0 is no darkening of the emissive (day time) texture and 1.0 is total darkening of the emissive texture|

### Polygon Offset
Setting | Default | Description | Requirement(s)
------- | ------- | ----------- | --------
``Polygon Offset``| 0 | Indicates to X-Plane what order the object should attempt to be drawn in, from farthest away from the player camera to closets. 0 tells X-Plane to automatically chose drawing order. Very useful for an object with many parts that are close together. See the blog post [The road to hell is paved with ATTR_poly_os](http://developer.x-plane.com/2006/09/the-road-to-hell-is-paved-with-attr_poly_os/) for a more detail |

### Cockpit Panel
Setting | Default | Description | Requirement(s)
------- | ------- | ----------- | --------
``Part Of Cockpit Panel``|Off|If checked, objects with this material will use the OBJs panel texture and will be clickable|
``Cockpit Region``|None|Defines which region this material should appear in. If set to none, no region will be used. The region number refers to the regions defined in X-Plane Layer's Cockpit Regions|

### Custom Properties
See Object->Custom Properties
