# Workflow Options

XPlane2Blender has a variety of tools that allow you to work in the way that is best for you. Here is an overview of those options, listed in a conversational manner.

## Layers Or Root Objects Mode?

Layers Mode and Root Objects Mode support all the same features and have no difference in performance.

![](/assets/workflow_tutorial_obj_export_mode_menu.png)

1. Layers Mode makes an OBJ per visible 3D View Layer. \*Any object and its children on that layer will be collected, with a few exceptions. Therefore, a .blend file using Layers Mode can produce up to 20 OBJs per scene. Scenery projects work well with Layers Mode, since all Blender Objects in an OBJ must be in 1 layer
2. Root Objects mode uses marked Objects and \*all their children \(and their nested children\) to make an OBJ. You can create any number of OBJs per file by using any number of Root Objects. Objects can be put into different 3D View Layers, however there are additional rules when using LODs. The ability to use 3D View layers independently of producing OBJs is favored by Airplane aritsts making complex cockpits

\*There are additional restrictions if an object is collected or ignored, described later

# How does each mode handle LODs?

In both modes, the amount and ranges of LOD "buckets" are sepecified in the OBJ settings.

![](/assets/workflow_tutorial_obj_lod_settings.png)

In Root Objects mode, 3D View layers 1-4 have a secial meaning if any LODs are specified. Objects in layer 1 get put in bucket 1. Objects in layer 2 get put in bucket 2 and etc, for the number of of LODs specified. Any objects outside of those layers are not exported. Objects on layers 5-20 will never be exported under any circumstance.  
  
For example:

> You make a root object, and specify 3 LODs. You put `Cube1`, `Cube2`, `Cube3`on layers 1, 2, 3, respectively. You put `Cube4`on layer 4 and `WorkLight` on layer 20. `Cube1`, `Cube2`, and `Cube3` will get exported, `Cube4` will not. If you were to specify 4 LODs `Cube4` will get exported. WorkLight will never be exported as long as it is on any layer between 5 and 20.

In Layers Mode, each Blender Object can be put into LOD buckets by using checkboxes on an Object's property tab. Some say this makes Layers Mode more flexible for using LODs than Root Object's use of layers 1-4.

![](/assets/workflow_tutorial_obj_lod_bucket_choice.png)

# How should I use .blend files?

Some people like

> 1 .blend file = All the .OBJ files for 1 airplane

or

> 1 .blend file = The .OBJ for 1 scenery asset

or

> 1 .blend file = The .OBJs for multiple scenery assets

A project can use multiple .blend files, each with multiple scenes, and each Scene can be in Layers Mode or Root Object Mode! Most people, however, keep things very simple - 1 .blend file with 1 Scene is enough

## How does the exporter search for Blender Objects to include in the OBJ?

Excluding all propreties and combinations of settings which could cause a Blender Object to be ignored for export:

* In Layers Mode, the exporter will find all objects and their children in the current scene on each layer.
* In Root Object the exporter will find all the specially marked "Root Objects" and their children.

# How can I organize my project's Blender Objects?

* Armature and Empty datablocks can be used to invisibly group and organize Meshs, Lamps, etc. If using Armatures, children can be parented to Armature's bones, or to the Armature datablock itself

* Advanced trick: a Blender Object can be on multiple 3D View Layers. This may be confusing to keep track of or impossible depending on your export mode and LOD setup, but it can reduce duplicating data across layers

* Don't forget about naming you Blender data well!

Technically, Meshes and Lights can also be tools for grouping, but they will export directives in the OBJ which isn't recommend if all you are trying to do is organize your Blender Objects

# How can I temporarily disable or enable which Blender Objects get exported?

In order of most local to most gobal:

1. For Layers Mode: If an object is hidden in the outliner, XPlane2Blender will skip exporting it and its children
2. For Layers Mode: each Blender Object has a "Export Mesh In Layers" \(currently misnamed and misdescribed\), which acts as a second version of Blender's 3D View Layers. The layer the object is in must be visible AND it must be enabled in "Export Mesh In Layers". This allows you to see the Mesh or Lamp in the 3D View, but still not have it be in the OBJ. \(Most people never use this\)
3. Put a Blender Object in a Layer or Root Object that isn't being exported \(or move a Blender Object entirely out of any Root Object's hierarchy of children\)
4. Move a Blender Object to a different Scene. The exporter only inspects objects in the current scene

# How can I temporarily disable or enable an OBJ from exporting?

In order from most local to most global:

1. For Layers Mode: Layers Mode only exports visible layers, so, only make the layers you intend to export visible!
2. In the OBJ settings \(where the name, export type, and lods are set\), in the Advanced Settings section there is an Export Checkbox. If unchecked, the OBJ will not be exported.![](/assets/workflow_tutorial_obj_export_checkbox.png)

# Which export method should I use?

The menu option \(`File -> Export -> X-Plane Object (.obj)`\) and the Export OBJs are the same in all regards except that the file menu allows you to export without saving first and export with any starting location. The Export OBJs button always uses the .blend file's folder as the starting location. Each Scene must be exported seperately.

# It is your choice!

With all these options, you are free to work in a variety of ways. The most important thing is to start! All these options can be changed later without losing progress or much time, so start simple and expand as needed. We can't wait to see what you create!

