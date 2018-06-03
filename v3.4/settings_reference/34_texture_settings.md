# Texture Settings
XPlane2Blender does not actually have any texture settings. However, certain Blender settings affect the export and even creation of new textures.

## What Textures and Materials Mean to X-Plane
As stated before, very little Blender information related to materials actually gets written to an OBJ. Instead, most of what changes what an object looks like in Blender comes from Texture work.

An OBJ file does not contain the texture, but rather, the path to the image file. **Only ``.png`` and ``.dds`` file types are allowed.** ``.dds`` files have special considerations, see the Further Reading at the bottom.

### Types of Textures
#### Albedo (day time texture)
An the albedo texture

## Relavent Blender Settings
None

### Texture Datablocks
``Material Texture Slots`` - **A list of texture slots. XPlane2Blender will inspect these and attempt to use them during export. Each slot must be an "Image or Movie" type.** The order of the slots is not important.

#### Image
``Source`` - **Can be Generated or "Single Image"** Generated textures must be compositable and saved as a real file to be referenced in an OBJ
``Image/Movie File Name`` - **If ``Source`` is "Single Image", this is the file path of the image.** OBJs refer to their images relative to their own location, not absolute harddrive locations, therefore you should keep source names relative to the .blend file to avoid surprises.
	For instance, if your texture is located at ``C:\Users\Me\images\landing_gear.png`` and your OBJ will be saved at ``C:\Users\Me\planes\new_project\gear.obj``, the OBJ will tell X-Plane to look for its texture "two folders up, then into a folder called images, and there will be landing_gear.png", aka ``..\..\images\landing_gear.png``, instead of the exact file path on your harddrive. Should you move your project to another folder that can't follow those steps, X-Plane will complain about invalid paths in your OBJ. The lesson is, *be neat and deliberate or be confused.*

### Mapping
``Coordinates`` - **Must be set to UV**
``Map`` - **Every texture must have a UV Map**

### Influence
XPlane2Blender uses which influence options to determine the purpose of each texture. This is important for many parts XPlane2Blender, from Autodetect Textures, Composite Normal-Textures, which OBJ attributes to write, and certain validations.

``Diffuse->Color`` - **XPlane2Blender considers textures with this checked to be the albedo (daytime) texture.** The actual value is not used
``Shading->Emit`` - **XPlane2Blender considers textures with this checked to be the lit (night time) texture.** The actual value is not used
``Specular->Intensity`` - **XPlane2Blender considers textures with this checked to be the specular texture.** The actual value **is used** to accumulate the total specularity of all the material's texture slots and the material's ``Specular Intensity`` (mklink) the material along with
``Geometry->Normal`` - **XPlane2Blender considers textures with this checked to be the normal texture.** The actual value is not used

## Further Reading
OBJ8 Spec Sections
- [TEXTURE APPLICATION](https://developer.x-plane.com/article/obj8-file-format-specification/#TEXTURE_APPLICATION)
- [TEXTURE](https://developer.x-plane.com/article/obj8-file-format-specification/#TEXTURE_lttex_file_namegt)
- [TEXTURE_LIT](https://developer.x-plane.com/article/obj8-file-format-specification/#TEXTURE_LIT_lttex_file_namegt)
- [TEXTURE_NORMAL](https://developer.x-plane.com/article/obj8-file-format-specification/#TEXTURE_NORMAL_lttex_file_namegt)

### DDS Format
Developer Blog Articles
- [DDS Revisited In X-Plane](https://developer.x-plane.com/2012/01/dds-revisited-in-x-plane-10/)
- [DDS and V10 - What Does It Do?](https://developer.x-plane.com/2012/11/dds-and-v10-what-does-it-do/)
- [Do Not use DDS as an Editing Format](https://developer.x-plane.com/2012/01/do-not-use-dds-as-an-editing-format/)
- [The Case For DDS](https://developer.x-plane.com/2007/08/the-case-for-dds/)

Other Tools
- [DDSTool Manual](https://developer.x-plane.com/docs/scenery/ddstool-manual/)
