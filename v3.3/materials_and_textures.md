# Materials and Textures
## Materials

As already mentioned in the previous chapter all objects that you want to export need materials assigned to them. It will only export the first material assigned to an object. 

### What will be exported?

Xplane2blender can only export the following material properties to Xplane:

- diffuse color
- diffuse intensity
- specular intensity (specular size will always be 128)
- Emit value


![](images/docs-3.2x-materials-and-textures_1.png)

### X-plane related material properties

You have additional material properties under the Xplane panel in each material:

![](images/docs-3.2x-materials-and-textures_2.png)

- **draw**: when disabled the surface will be invisible in xplane, but it will still be physically there. Use this for low poly proxy manipulator handles for example. Using high poly objects for manipulators is not recommended, as it's pretty expensive.
- **override specularity**: when enabled you can set specularity values above 1.0 with the shiny ratio to simulate very glossy surfaces.
- **use alpha cutoff**: If enabled transparent parts of the texture that are below a certain alpha value will be cut away/hidden and all other parts will be fully opaque.
- **surface type**: The material can represent a physical surface of some kind. This is especially usefull for Scenery objects.
- **camera collision**: If checked, the objects having the material assigned will collide with the camera. Use this to restrict camera movement in the cockpit.
- **polygon offset**: This is usefull for scenery objects that lie on top of other geometry like a runway for example. In that case you can set the polygon offset to a value greater then 0 to force it to be drawed on top the underlinying geometry.
- **override light level**: If checked you can override the amount/brightness of the night texture to be used for the material when a certain dataref reaches values. Value 1 tells the sim to set the light level to 0 when the dataref has that value. Value 2 sets the light level to 1 (full) when the dataref has that value. The light level will interpolate between value 1 and value 2. You can use this to for example create glowing buttons or custom cockpit lighting.
- **part of cockpit panel**: if checked objects with the material will be treated as part of the cockpit panel texture. For historical reasons you still can select which one of 4 regions the material should use, however as that was a workaround for very old hardware you can leave it at "none" to use the full panel texture in the material. If you want to use single regions you need to set them in the X-Plane Scene settings for the particular X-Plane layer.
- **custom properties**: You can add any additional property to the material that will be written to the OBJ file. This is usefull to for example include properties in an OBJ file that XPlane2Blender currently does not support, but you don't want to edit the OBJ file after every export to implement these new properties. A property has the following settings:<br/>**name** - the name of the property, **value** - the value of the property, **reset** - another property reseting/disabling the given property, this is important because otherwhise all things that are exported after this material will still have the given property.


## Textures

**The textures you assign to a material will not be used for export.**

This has a very simple reason:

As X-Plane's OBJ files only support the use of **one texture per OBJ file** and XPlane2Blender exports **one layer as a single OBJ file**,
we define the texture to be used for an OBJ file in the X-Plane scene settings for the individual layers.

### Setting texture(s) for a layer

[See the previous chapter for how to assign a texture to a X-Plane layer.](./docs-3.2x-Export-OBJ-files#2-configure-a-x-plane-layer)

The texture(s) will only be visible on objects that are UV unwrapped.
To learn how to UV unwrap in Blender read the following pages: http://wiki.blender.org/index.php/Doc:2.6/Manual/Textures/Mapping/UV

### Getting a live preview for the in-game textures

To get a direct feedback of how a texture will look like in X-Plane within the Blender viewport you can do the following:

1. In the viewport open the Properties shelf by hitting "N"
2. Scroll to the panel labeled **Shading**
3. Set the value of the dropdown to **GLSL**. This will display the textured view mode of the viewport with advanced OpenGL shading called GLSL, which is very close to the shading within X-Plane with "per pixel lighting" turned on.
4. Enable "Backface Culling" to hide faces facing backwards as X-Plane does.
5. Set the viewport shading to **Texture** by hitting ALT+Z
6. Now you need to assign the correct textures to all materials you want to preview

![](images/docs-3.2x-materials-and-textures_3.png)

#### Texture preview for the default texture / day texture
1. Add a texture of type "Image or Movie" to the material you want to preview in the viewport
        ![](images/docs-3.2x-materials-and-textures_4.png)
2. Select the texture file you've set as the Default / Day texture as the image
3. Under **Mapping** select **UV** as Coordinates and keep Projection at "Flat".
4. Under **influence** check **Color** and set it's value to 1.0<br/>
        ![](images/docs-3.2x-materials-and-textures_5.png)
5. Leave the **color space** at **sRGB** as this fits for most cases and will prevent color shift in the viewport
        ![](images/docs-3.2x-materials-and-textures_6.png)

#### Texture preview for the normal/specular texture
1. Add a texture of type "Image or Movie" to the material you want to preview in the viewport
        ![](images/docs-3.2x-materials-and-textures_7.png)
2. Select the texture file you've set as the normal / specular texture as the image
3. Under **Mapping** select **UV** as Coordinates and keep Projection at "Flat".
4. Under **influence** uncheck **Color** and check **Normal** and set it's value to 1.0<br/>
        ![](images/docs-3.2x-materials-and-textures_9.png)
5. Under **Image Sampling** uncheck **Alpha: Use** and check **Normal Map** and as normal map type select **Tangent**
6. Leave the **color space** at **sRGB** as this fits for most cases and will prevent color shift in the viewport
        ![](images/docs-3.2x-materials-and-textures_8.png)

#### Texture preview for the specular texture
In X-Plane the normal textures alpha channel is used as the specular texture defining the specular intensity. In Blender we cannot use the Alpha channel like that and thus have to extract the alpha channel from the normal / specular texture as a grayscale image. You can do this using your Image-Editor or also using Blenders compositor nodes. However I guess you will probably already have a grayscale specularity image and actually need to manually set it as alpha channel for the normal map.

1. Add a texture of type "Image or Movie" to the material you want to preview in the viewport
2. Select the grayscale image with the specularity texture you've used for the alpha channel in the normal / specular texture
3. Under **Mapping** select **UV** as Coordinates and keep Projection at "Flat".
4. Under **influence** uncheck **Color** and check **Specular Intensity** and set it's value to 1.0
5. Leave the **color space** at **sRGB** as this fits for most cases and will prevent color shift in the viewport

## Some Material / Texturing tips

### One material, multiple OBJ textures
If you use the same material within layers/OBJ files that do not use the same texture and still want to preview both textures in the viewport you need to duplicate the material for the other layer. I've found it best practise to prefix the duplicates with the OBJ file name. For example fuse_chrome and wings_chrome.

### UV unwrapping of multiple objects for a single texture

As each OBJ file can only contain one texture but consists of multiple individual objects that all share this texture one needs to unwrap all those objects in a way so theire UV coordinates do not overlap. Blender has a usefull feature that makes this easier.

1. To make this work you need to set the same Image in the UV/Image-Editor in Edit-Mode for every object in the layer
2. Select all objects within the layer and then additionally select the object you want to UV unwrap. This way the object will be the **active** one.
3. Go into edit-mode and in the UV/Image-Editor under **View** check **Draw other objects**. This will display the UVs of all other selected objects that have the same image assigned in the UV/Image-Editor together with the UVs of the currently edited object.


### Texturing workflow
Sometimes its hard to get a texture look realistic just by painting it in your Image-Editor. Things can easily look distorted due to the UV distortion, baked in shading like ambient occlusion can look artificial if you simply paint it by hand, baked in reflections can look artificial.

To overcome this problem you can aim for a texturing workflow that makes use of Blenders texture baking feature and compositor nodes.

In general the workflow looks like this:

1. Create duplicates of the UV unwrapped low-poly in-game objects within one layer you want to texture and move them to a layer that is not used for OBJ export
2. You can now add subsurface modifiers or multires modifiers to the objects to add aditional detail / smoothness to the duplicates. Subsurf can be controlled by edge crease values. The important thing is to preserve the UV mapping in the duplicates.
3. You now can add multiple materials with multiple textures to the duplicates and make use of Blenders internal renderer to create realistic looking surfaces for your duplicates
4. Finally you render bake the objects to a single texture by selecting the duplicate and in the render properties under **Bake** select **Full render**, uncheck **Selected to Active** and hit **Bake**. For more information about this read the following pages: http://wiki.blender.org/index.php/Doc:2.6/Manual/Render/Bake
5. To bake normal maps you need to bake from **Selected to Active** from you high poly duplicate to the low-poly in-game object or you can take my preset at BlendSwap for normal map baking without the common problems: http://www.blendswap.com/blends/node-setups/tangent-space-normal-map-baking-from-two-object-space-normal-maps/

There is a lot of try and error with render baking and you will need to fine adjust your materials allot, but basically it will make your texturing work look more realistic and easier.

#### Some tips for render baking

- mirror reflections work best if you set Fresnel to 0.0 and the Reflectivity higher then you would in a regular render
- for better outer reflections add an image texture containing an environment map containing a simple sky and ground and set its mapping to **Reflection**, its influence to **Color** and the Blend to **Screen**.
- render baking is way slower then regular rendering, so try to avoid the expensive mirror reflections with a gloss amount lower then 1.0
- render baking does not use anti-aliasing! That's why you need higher sample rates for ambient occlusion, Area-Lights, Ray-traced soft shadows and things like mirror reflections. It's best to post-process the render baked images with a image-based antialising in your Image-Editor to reduce noise in the texture and to be able to reduce sample rates during render baking.


If you think this is a good thing [buy me a beer](../../Donations).
