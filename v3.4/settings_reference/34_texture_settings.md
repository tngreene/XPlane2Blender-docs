# Texture Settings
XPlane2Blender does not actually have any texture settings. However, certain Blender settings affect the export and even creation of new textures.

## What Textures and Materials Mean to X-Plane
As stated before, very little Blender information related to materials actually gets written to an OBJ. Instead, most of what changes what an object looks like in Blender comes from Texture work.

An OBJ file does not contain the texture, but rather, the path to the image file. **Only ``.png`` and ``.dds`` file types are allowed.** ``.dds`` files have special considerations, see the Further Reading at the bottom.

### Types of Textures
#### Albedo (day time) Texture
An the albedo texture

#### Lit (night time) Texture

#### Specular Texture

#### Normal Texture

## Relevant Blender Settings
None

### Texture Datablocks
``Material Texture Slots`` - **A list of texture slots. XPlane2Blender will inspect these and attempt to use them during export. Each slot must be an "Image or Movie" type.** The order of the slots is not important.

#### Image
- ``Source`` - **Can be Generated or "Single Image"** Generated textures must be composit-able and saved as a real file to be referenced in an OBJ
- ``Image/Movie File Name`` - **If ``Source`` is "Single Image", this is the file path of the image.** OBJs refer to their images relative to their own location, not an absolute path like ``C:\Users\Me\plane_project\images\landing_gear.png``. You should keep paths relative to the .blend file to avoid distribution problems. Blender uses ``//`` in paths to refer to "the folder the .blend file is in". Blender and XPlane2Blender also supports the use of ``..`` (meaning _one parent folder_) and ``.`` (meaning _the current folder_).

    For example: An image at ``//images/landing_gear.png`` would be read as "Starting at the folder the .blend file is in (``//``), looking in the folder ``images`` for the file ``landing_gear.png``. Naming a layer ``../test_objs/landing_gear.obj`` would export the OBJ ``landing_gear`` to the folder ``test_objs``, which is in the parent folder of the .blend file. No user folder or drive letter is referenced, making the project a lot more portable.

### Mapping
- ``Coordinates`` - **Must be set to UV**
- ``Map`` - **Every texture must have a UV Map**

### Influence
XPlane2Blender uses which influence options to determine the purpose of each texture. This is important for many parts XPlane2Blender, from Autodetect Textures, Composite Normal-Textures, which OBJ attributes to write, and certain validations.

Property | Texture Purpose | Use of Value
---------|-----------------|--------------
``Diffuse->Color`` | Albedo (daytime) Texture | None
``Shading->Emit``  | Lit (night time) Texture | None
``Specular->Intensity`` | Specular Texture | Intensity value is used to accumulate the total specularity of all the material's texture slots (in addition to the material's own ``Specular Intensity``)
``Geometry->Normal``    | Normal Texture | None

## Further Reading
Blender Manual
- [Relative Paths in Blender](https://docs.blender.org/manual/en/dev/data_system/files/relative_paths.html?highlight=relative)

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
