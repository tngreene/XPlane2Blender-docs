# Workflow Options

XPlane2Blender has a variety of tools to allow you to work in the way that is best for you. Here is an overview of those options, listed in a conversational manner.

## Layers Or Root Objects Mode?

1. Layers mode uses Blender's 3D View layers to seperate OBJs. Therefore, a .blend file using layers mode can produce up to 20 OBJs. Great for scenery artists.
2. Root Objects mode uses Empty objects and a tree of parent-child relationships. With this, you can still Empties marked as "Root Object" Use Root Object mode and create any number of OBJs by specifying Root Objects and giving them children. Great for planes, since planes have complicated intricate parts that benifit from layering and show/hiding. LOD in root object mod

## What about LODs?

Layers mode uses checkboxes to assaign objects into buckets, Root Object mode uses their presence in Layer 1, 2, 3, 4 to specify what an object should be, which can be constricting.

# What about organizing my datablocks?

* Use Datablocks like Armatures and Empties to organize things in the outliner tree. You can use bone parent or Armature datablock parent.
* Use the 1 Scene = 1 Obj pattern
* Use the "each scene is 1 OBJ"

What about the relationship between OBJ files the .blend file?

* Generally, people like 1 .blend file = 1 airplane or 1 .blend file equals 1 scenery asset.

## I want to organize my stuff... \(combine as much as you'd like for greater fun and headaches!\)

1. Use multiple .blend files, linking and appending as needed
2. Use one .blend file full of DataBlocks, with single or multiple users
3. Use Empties to group things into hierarchies
4. Use Armatures to group things into hierarchies
5. Use Meshes or Lights to group things into hierarchies! \(Why would you do this though?\)
6. Sort DataBlocks into different layers. You can selectively export layers in Layers Mode. Remember in Root Objects Mode Layers 1, 2, 3, and 4 can have a special meaning.
7. Use Scene datablock for even greater separation of concerns
8. You can have each Scene make 1 or more OBJs!
9. You can have multiple scenes in a .blend file each choosing their own Export Mode!

With all of this you can have such semantics for your project as

> "One .blend file means one OBJ"

> "One layer means one OBJ"

> "One Root Object means one OBJ"

> "Each Scene in the .blend file means one OBJ"

> "Certain Scenes represent OBJs, others just represent organization"

and more!

## I want convenient ways to options to run the exporter to export all of my OBJs

1. The File 
   &gt;
    Export 
   &gt;
    X-Plane Object \(.obj\) \(which uses the current Scene\)
2. The Instant Export button \(which uses the current Scene\)
3. The Export All Scenes As OBJs Buttons \(planned, but maybe we better talking about that in light of how confusing this is getting...\)

## But most importantly, how will the exporter know what to take?

* In Layers Mode, the exporter will find all objects and their children in the current scene on each layer.
* In Root Object the exporter will find all the specially marked "Root Objects" and their children.

The exporter will never reach beyond the current scene, even following parent-child relationships.

