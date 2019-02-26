# Workflow Options

XPlane2Blender has a variety of tools to allow you to work in the way that is best for you. Here is an overview of those options, listed in a conversational manner.

## Layers Or Root Objects Mode?

1. Layers mode uses Blender's 3D View visible layers to seperate OBJs. Any object and its children in a layer that is being exported into an OBJ will be collected\*. Therefore, a .blend file using Layers Mode can produce up to 20 OBJs per scene. An Object's LOD buckets are chosen by checkboxes in the Object's property tab. Since each layer must contain all the Blender Objects that will go into that OBJ, simple scenery objects fit nicely in it. Layers mode's checkbox style of specifying LODs is much more flexible than in Root Objects mode
2. Root Objects mode uses marked Objects and \*all the children \(and their nested children\) to make an OBJ. You can create any number of OBJs per file by using any number of Root Empty Objects. Objects can be put into different 3D View Layers, however there are additional rules when using LODs. The ability to use 3D View layers independently of producing OBJs is favored by Airplane aritsts making complex cockpits

Layers Mode and Root Objects Mode support all the same features and it is easy to switch modes later on. The only difference is your preference of workflow.

## How does the exporter search for Blender Objects to include in the OBJ?

* In Layers Mode, the exporter will find all objects and their children in the current scene on each layer.
* In Root Object the exporter will find all the specially marked "Root Objects" and their children.

The exporter will never reach beyond the current scene, even following parent-child relationships.

\*There are additional restrictions if an object is collected or ignored. See below for more details

# How does each mode handle LODs?

In both modes, the ranges and amount of LOD "buckets" are sepecified in the OBJ settings. In Layers Mode, each Blender Object can be put into LOD buckets by using checkboxes on an Object's property tab. In Root Objects mode, layers 1-4 are special if any LODs specified. Objects in layer 1 get put in bucket 1. Objects in layer 2 get put in bucket 2. Etc, etc, etc.

# How should I structure my project?

Some people like

> 1 .blend file = All the .OBJ files for 1 airplane

or

> 1. blend file = The .OBJ for 1 scenery asset

or

> 1 .blend file = The .OBJs for multiple scenery assets

A project can use multiple .blend files, each with multiple scenes, and each Scene can be in Layers Mode or Root Object Mode! Most people, however, keep things very simple - 1 .blend file with 1 Scene is enough

# How can I organize my project's Blender Objects?

* Armature and Empty datablocks can be used to invisibly group and organize Meshs, Lamps, etc. If using Armatures, children can be parented to Armature's bones, or to the Armature datablock itself
* Technically, Meshes and Lights can also be tools for grouping, but they will export directives in the OBJ
* A Blender Object can be set to appear in multiple 3D View Layers. This may be confusing to keep track of, but is a great way to reduce copying and pasting between layers. Depending on your export mode and/or LODs, the use of 3D View Layers could have additional semantics to keep track of.

# How can I temporarily disable or enable which Blender Objects get exported?

In order of most local to most gobal:

1. For Layers Mode: If an object is hidden in the outliner, XPlane2Blender will skip exporting it and its children
2. For Layers Mode: each Blender Object has a "Export Mesh In Layers" \(currently misnamed and misdescribed\), which acts as a second version of Blender's 3D View Layers. The layer the object is in must be visible AND it must be enabled in "Export Mesh In Layers". This allows you to see the Mesh or Lamp in the 3D View, but still not have it be in the OBJ. Most people never touch this.
3. Put a Blender Object in a Layer or Root Object that isn't being exported \(or move a Blender Object entirely out of any Root Object's hierarchy of children\)
4. Move a Blender Object to a new or different Scene. The exporter only inspects objects in the scene it started from.

# How can I temporarily disable or enable an OBJ from exporting?

In order from most local to most global:

1. For Layers Mode: Layers mode only exports visible layers. Simply don't enable the layer you don't want to export.
2. In the OBJ settings \(where the name, export type, and lods are set\), in the Advanced Settings section there is an Export Checkbox. If unchecked, the OBJ will not be exported.

With all these options for temporarily showing/hiding Blender



## 



