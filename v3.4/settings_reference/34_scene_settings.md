# Scene Settings
To access, navigate to Blender's Properties Pane and click on the Scene Icon [icon], and scroll to the X-Plane panel.

## Basic Settings
### Export Objs Button
This button will export the .blend file and save the exported .obj files relative to it. **The only difference between using this button and using the File->Export->X-Plane Object (.obj) menu option is that the menu option gives you an export dialog box to choose your export destination. Exported Objs will be the same using either method.**

### X-Plane Version
**Latest released version of X-Plane by default.** A drop down menu with versions of X-Plane to target. The behavior of the plugin, and contents of exported OBJs may changed based on it. In addition, certain parts of the UI may only be shown under certain versions. For instance, "Blend Glass" will only appear as a Blend option when the X-Plane Version is set to ``11.0x`` or higher.

### Export Mode
A drop down menu with two options: "Layers" and "Root Object", **"Layers" by default**. These represent how the exporter will collect blender objects for processing into OBJs.

#### Layers Mode
In "Layers" mode, each of Blender's [Object Layers](https://docs.blender.org/manual/en/dev/editors/3dview/object/properties/relations/layers.html) are combined with their corresponding X-Plane Layer (1st Blender layer goes with X-Plane layer 1, 2nd Blender layer goes with X-Plane layer 2, etc). The Blender layer's list of objects that are visible in it gets combined with the [X-Plane Layer's settings](mkdown) and is exported as a complete OBJ.  Non-visible Blenders Layers are not combined with their corresponding X-Plane Layers and do not get exported. In "Layers Mode" the settings for each X-Plane Layer is shown in the scene settings.

##### Caveats
You are limited by Blender's maximum of 20 object layers. All objects being collected must be visible on the same layer as being exported, including children. For example: Cube A, B, and C are on layer 1. Cube C has a child Cube D. Cube D must be visible on layer 1 as well. Making objects visible in multiple layers is not recommended because it can get messy fast. [fact check]

##### Example Workflow
An example use of this workflow is a "warehouse collection" project. Models of warehouses (small, medium, large, and mirrored variants) are each organized into layers. Layers mode is a good choice because it would be a collection of less than 20 things to model, where having many being visible would not be a problem or a distraction - it is not a necessary part of an artist's workflow to use the Object Layer Visibility feature to repeatedly show or hide parts of the model since the warehouses can be spread apart.

#### Root Object Mode
In "Root Object" mode, Blender Object's parent-child relationships are used to establish which X-Plane layers groups of objects should be exported together with. In the [Blender Outliner](https://docs.blender.org/manual/en/dev/editors/outliner.html?highlight=outline), top level [Empty Data Blocks](https://docs.blender.org/manual/en/dev/modeling/empties.html) [icon] can be set to be root objects. The tree of children of the root object are collected as the objects to be exported to the OBJ. Blender Object Layers are irrelevant in the process.

##### Caveats
A root object cannot contain a root object.

##### Example Workflow
An example use of this workflow is an airplane with many parts. An airplane may have more than 20 parts, and much of them are nestled together making it hard to work on the model without hiding many parts of it. It would be very annoying to have to continually enable and disable the Blender Object Visibility Layers to make each component export which, fortunately, is not necessary in "Root Object" mode. You are free to use that feature of Blender however you wish.

### Compile Normal-Textures
**Shown always, only affects layers where ``Autodetect Textures`` is on. On by default**. A checkbox which turns on or off the compiling of normal textures from existing normal and/or specular textures as needed. Given a detected normal texture, specular texture, or both, XPlane2Blender will create a combined image and save it to disk (with the suffix "_nm", "_nm_spec", or "_spec" depending on what was used in the generated file). This will be referenced in the OBJ as a replacement for the regular normal or draped normal file.

See [materials] for more information.

## Advanced Settings
### Optimize
**On by default**. A checkbox which turns on or off the remove duplicate vertices optimization. Removing duplicate vertices can increase performance in X-Plane, but may also increase export time. All OBJs will render the same regardless of optimization.

### Print Debug Info To Output, OBJ
**On by default**. A checkbox which changes what debug information gets printed and where. During export, XPlane2Blender keeps a log of events, broken down into four categories: *ERROR*, *WARNING*, *INFO*, and *SUCCESS*. *ERROR* and *WARNING* events are always printed, *INFO* and *SUCCESS* events statements are printed only when the checkbox is checked.

Also, when this box is checked, information such as mesh names, vertices index numbers, and exporter version numbers are printed as comments in the .obj. They are invisible and meaningless to X-Plane, but extremely useful for humans reading or debugging them.

### Create Log File
**Requires ``Print Debug Info To Output, OBJ`` turned on. Off by default**. A checkbox which indicates whether or not the internal log will also get saved to a text file ``xplane2blender.log``. It is located in the same directory as the saved .blend file. 
