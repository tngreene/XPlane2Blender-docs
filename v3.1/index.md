
# Scenery and Cockpit import/export scripts for Blender

## Preface

This is the final version of Xplane2Blender v 3.10. It's been tested and works with Blender 2.49 on Mac, Windows, and Linux. Development of this script is no longer done by Marginal, but collectively and in an Open-Source manner. So please file requests and issues at the project website.

## Overview

Blender is an open source 3D object editor for Windows, Mac and UNIX.

These Blender scripts export models created in Blender to X-Plane v7, v8, v9 or CSL .obj format.

The scripts also import existing X-Plane v6, v7, v8, v9 and CSL .obj files and X-Plane v7, v8 and v9 .acf airplanes into Blender.

## Requirements

Runs on Windows 2000 or later, Mac OS 10.3.9 or later, and Linux.

Requires Blender 2.45 or later:

### Windows:

[Download](http://www.blender3d.org/Download/) and run the "Installer" build of Blender.

### Mac OS 10.5:

[Download](http://www.blender3d.org/Download/) the "Python 2.5" build of Blender for Intel or PPC.
To install, copy the Blender application out of the disk image eg to your /Applications folder.

### Mac OS 10.3 & 10.4:

[Download](http://www.blender3d.org/Download/) the default "Python 2.3" build of Blender for Intel or PPC, unless you have installed Python 2.5.
To install, copy the Blender application out of the disk image eg to your /Applications folder.

### Linux:

Most distros come with Blender, so you can install it via your package manager (eg Synaptic, YaST, YUM).
Or [download](http://www.blender3d.org/Download/) the build that corresponds to the version of Python that is installed on your system.

## Changes for 3.10 Final

The two major changes since Beta 3 are:

* support for ATTR_light_level (this allows you to assign an object in Blender with the ability to independently "turn on" the LIT texture, based on a given dataref.)
* Fixed the multiple texture bug that was still present in Beta 4. This applies ONLY to the cockpit .obj, since it's the only one to support 2 textures. Now the script correctly interprets which of the textures is assigned to which animated mesh in Blender, and exports it accordingly.

## ATTR_light_level

The way you use ATTR_light_level is outlined in detail on the obj8 spec website. That site describes what the resulting .obj file would look like in a text editor. This script allows you to store that information in Blender, so that it can be saved as part of your aircraft's source files.

What this feature does is it allows you to swap the daytime and nighttime (LIT) textures on a per-mesh basis, triggered by a dataref of your choice. This allows you to, for example, build 3D buttons that "light up" when their particular dataref is triggered.

Here's how you would do it in Blender. Let's say we're dealing with a 3D "fuel pump" button that's supposed to light up when the fuel pump is on. First, you'd have to have a daytime and LIT version of the texture. Without ANY CHANGES, this button's behavior would be such, that when X-Plane goes from day-mode to night-mode, this button's texture would swap from daytime to LIT texture. However, you can override this, and cause the texture swap to take place when the dataref for the fuel pump is called up. With the button selected (pink) in Blender, call up the "Game Logic" button (F4 keyboard shortcut). Click on "Add Property" and type "ATTR_light_level" (no quotes) into the space labeled "Name:" Then select "String" from the drop-down menu directly to the left of this blank. Now enter the dataref for the fuel pump into the blank space to the right. (in this case, it would be "sim/cockpit/engine/fuel_pump_on").

You can now save this .blend file, and the lighting information you've entered for this button should be grabbed by the new exporter. 

## Tutorials

This document is a reference and assumes familiarity with Blender. There is a detailed series of video tutorials on YouTube that aim to provide developers with the background and techniques needed to make basic planes, and to continue making detailed planes using this script and Blender. The [first 14 tutorials](http://www.youtube.com/watch?v=Os7O-uPhIHk&feature=PlayList&p=83BC4217746786FF&index=0&playnext=1) are aimed at familiarizing you with PlaneMaker.

The [following tutorials](http://www.youtube.com/watch?v=VPTsK3WLTxI&feature=PlayList&p=DB0F4B925CF9169C&index=0&playnext=1) showcase how to create and animate detailed .obj files that you can append to your .acf file, and even allow you to replace PlaneMaker components, which are low-res, low-polygon parts, with highly detailed, intricately textured .obj files.

* [Using Blender to create X-Plane scenery](http://marginal.org.uk/x-planescenery/tutorials.html)
* [Blender3D: Noob to Pro](http://en.wikibooks.org/wiki/Blender_3D/Noob_to_Pro)
* [The Blender Manual](http://wiki.blender.org/index.php/Manual)

## Installation

Run Blender to check that it is installed correctly. If the Blender window appears "blurry" turn off anti-aliasing in your video card's OpenGL settings and re-start Blender.

Now close Blender.

### Windows Vista:

Extract the contents of the zip file to a new (temporary) folder.
Right-click on the file install.cmd and choose Run as administrator.
(This installs the scripts in the folder %HOME%\blender\scripts if it exists, otherwise in the copy of Blender that is associated with .blend files).

### Windows 2000/XP:

Extract the contents of the zip file to a new (temporary) folder.
Double-click on the file install.cmd.
(This installs the scripts in the folder %HOME%\blender\scripts if it exists, otherwise in the copy of Blender that is associated with .blend files).

### Mac OS:

Double-click on the file install.command.
(This installs the scripts in the folder ~/.blender/scripts if it exists, otherwise in all copies of Blender that the Finder knows about).

### Linux:

Start a shell window, and type:
mkdir -p ~/.blender/scripts

Extract the contents of the zip file to this folder.

(Re)start Blender. This file can now be viewed by choosing Help → X-Plane in Blender.

You can now delete the temporary folder.



If the above mentioned installation of the scripts does not work, you can still open these Python-scripts in Blender's text-editor window, and run each script by pressing “Alt+P.” This method can also save time. If, for instance, you keep the Python-script in one of Blender's text-editor windows, it is easier to call it up via the “Alt+P” key command, than by browsing to the appropriate plug-in via the pop-up menus in the Python window.

The two most commonly used Python scripts once development is in full swing, are the “XplaneAnimObject.py” and the “XplaneExport8.py.” I've found that keeping these scripts in a small window in your Blender project makes animating and exporting X-Plane .obj's faster and easier.

## Importing objects

First, move the 3D Cursor to where you want the imported object to be placed. Usually you'll want the object to be placed at the origin so just press Shift C to centre the 3D Cursor at the origin.

Choose File → Import → X-Plane Object, select a .obj file and press Import OBJ.

The scenery is imported at the 3D Cursor position.

You can import multiple .obj files and re-export them as a single file. But note that the X-Plane .obj file format only supports the use of one texture file, so you'll have to create a single larger file containing all required textures - see below. Or you can have Blender create this single file automatically by selecting all the objects and, in a UV/Image Editor window, choosing Image → Consolidate into one image.

## Importing planes

First, move the 3D Cursor to where you want the imported plane or weapon to be placed. Usually you'll want it to be placed at the origin so just press Shift C to centre the 3D Cursor at the origin.

Choose File → Import → X-Plane Plane or Weapon and choose whether to import the plane or weapon so that the "reference point" is located at the 3D Cursor (for making cockpit & misc objects) or so that the "centre of gravity" is located at the 3D Cursor (for making CSLs and static scenery).

Then select a .acf or .wpn file and press Import ACF or WPN.

The script creates up to three versions of the plane or weapon in Blender, one in each of layers 1, 2 and 3. The versions in layers 2 and 3 use approximately 1/10th and 1/100th of the number of faces compared to the version in layer 1. See "Level of Detail" below for an explanation of why it does this.

Imported planes need some tweaking before you can export them as scenery or as a CSL object; see "Tweaking planes" below.

## Exporting objects

First, choose File → Save As… and save the .blend file in the aircraft or scenery folder where you want the .obj file to end up. Then choose:

    File → Export → X-Plane CSL Object or 
    File → Export → X-Plane v7 Object or 
    File → Export → X-Plane v8/v9 Object 

The object is exported in the same folder and with the same name as the current Blender file, but with a .obj extension. Blender may display some informational messages - click on one of these messages to see which object(s) the message refers to.

If there is an error then the scripts will attempt to identify and highlight the offending Blender object(s).

*cs*: These objects are intended for use with multi-user plugins such as [XSquawkBox](http://www.xsquawkbox.net/xsb/) or [X-IvAp](http://www.ivao.aero/softdev/X-IvAp/).
*v8*: These objects are supported by X-Plane versions 8.20 and later.
*v9*: These objects are supported by X-Plane versions 9.00 and later.

## Creating X-Plane scenery

* Find and open the Custom Scenery folder inside of your X-Plane installation.
* Create a subfolder with the name of the scenery package that you're making.
* Save your Blender file in this subfolder folder with a descriptive name, eg:
      X-Plane/Custom Scenery/EGLL/house.blend

      The X-Plane .obj file will be exported to the same place, ie:

      X-Plane/Custom Scenery/EGLL/house.obj

## Tweaking planes

Imported planes need to be positioned correctly on the ground for use as static scenery (don't do this if you're making a CSL or cockpit object):

* Select layers 1-3, select all objects and position the plane so that its undercarriage is sitting directly on the ground (represented by the x/y axes).
* You may also need to rotate the plane slightly so that all wheels are level; press r and move the mouse to rotate the plane so that its undercarriage is sitting directly on the ground. Click to set the plane's position.

The primary file for textures is named airplane_paint. Most planes also use textures from a secondary file named airplane_paint2. Objects that use textures from the secondary file are imported with "*" after their name to make them easier to identify in Blender's Outliner window.

The X-Plane .obj scenery file formats only support the use of a single file for textures, up to 1024x1024 pixels in size. If your plane only has a few simple objects that use textures from airplane_paint2 then you should re-texture these objects to use airplane_paint, following the same procedure described below for weapons and misc objects. If that is not feasible you can use this procedure to make the plane use textures from a single file:

* Save your Blender model.
* In an image editor application, resize airplane_paint and airplane_paint2 to 512x512. (You don't need to save these resized versions).
* Create a new bitmap file 1024 pixels wide and 512 pixels high.
* Paste the resized airplane_paint into the left half of this bitmap.
* Paste the resized airplane_paint2 into the right half of this bitmap.
* Save the bitmap file in the same folder and with the same name as your .blend file. If you're making a CSL object then you must save in PNG format.
* If your plane uses night-time textures then repeat this procedure for the _LIT bitmap files.
* In a Blender UV/Image Editor window choose Image → Merge _paint and _paint2.

If your imported plane uses weapons or misc objects then each of these will use an additional bitmap file. Weapons are imported with their names starting with "Wnn" and objects with their names starting with "Onn". Also note that reduced-LOD versions of weapons and misc objects may be present in layers 2 and 3.

Open an Outliner window and choose View → Show Outliner. For each mesh that has a name starting with "Wnn" or "Onn" or ending with "*", either:

* Delete the mesh, or
* Copy the required textures to an unused area in the primary bitmap file and use the UV/Image Editor window to map the new copy of the textures to the mesh's faces.

Consider performance issues when the plane is rendered in X-Plane. Ask yourself the following questions:

* Most important: Do you really need fully detailed 1024x1024 textures for your plane? Video memory is used up by terrain and object geometry and textures. Once you run out of video memory the GPU has to fall back to main memory, and this really slows things down. One 1024x1024 texture uses 4MB of video memory. Some people are running X-Plane on computers with only 32MB of video memory, so one 1024x1024 texture at "extreme res" in X-Plane uses 1/8th of their video memory. Consider resizing the texture file in an image editor program to half or even quarter size. Use Image → Replace to use the new texture file.
* Does the model have hidden faces? Some versions of X-Plane don't handle hidden faces in v7 scenery objects very well and they also a cause a small performance hit. Look for things like wings or misc bodies that are partially or wholly buried in the fuselage and delete any wholly hidden faces before exporting.
* Do you really need all that detail? Consider deleting details like flap tracks, antennae etc before exporting. This especially goes for the lower Level of Detail versions of the plane in layers 2 and 3 which are only viewed in X-Plane from >1000m and >4000m respectively.

## Creating 3D cockpits

X-Plane 3D cockpits are just normal v7, v8 or v9 scenery objects except that cockpits can't contain multiple Levels of Detail, so only objects in Blender layer 1 are exported. If you want to keep objects in your Blender scene for reference but which you don't want to export - eg the plane fuselage - then put them in layer 4 or greater before exporting.

Choose File → Save As and save the blender file in the same folder as your plane's .acf file with the name airplane_cockpit.blend, airplane_cockpit_INN.blend or airplane_cockpit_OUT.blend (where airplane is the name of your plane's .acf file):

* X-Plane displays airplane_cockpit.obj in both internal and external views.
* X-Plane displays airplane_cockpit_INN.obj only in internal views.
* X-Plane displays airplane_cockpit_OUT.obj only in external views. If you create an airplane_cockpit_INN.obj and/or airplane_cockpit_OUT.obj then you should not create airplane_cockpit.obj.

You will usually want to import your plane into Blender to act as a reference and/or starting point for your cockpit. Delete any plane parts that you don't need in creating your cockpit - you only need to keep the fuselage itself plus any relevant Misc Bodies. After import, your cockpit uses the same texture file as your plane, ie airplane_paint. Choose Image → Replace in a UV/Image Editor window to use a different texture file, which can be named anything you like (but no spaces) and which should live in the same folder as your plane's .acf file.

To make your 3D cockpit appear in X-Plane, on the Standard → Viewpoint → View screen in PlaneMaker, check the show cockpit object in: INSIDE views, exact forwards option. To hide the 2D cockpit altogether, also check the show cockpit object in: PANEL views, exact forwards option; hiding the 2D cockpit means that you no longer have to leave a large part of the Panel Texture transparent to represent the windscreen, which gives you more room on the Panel Texture for instruments.

### Cockpit instruments

To construct moving cockpit instruments paint the …/cockpit/-PANELS-/Panel.png texture in an image editor application and place instuments in PlaneMaker as as you would for a 2D panel (but bear in mind that only the top 768 lines of the Panel Texture can be used in the 3D cockpit in X-Plane versions prior to 8.20). The Panel Texture can by 1024×any size in X-Plane v8, and any size up to 2048×2048 in X-Plane v9. Normally you can only use a single file to texture your X-Plane objects. But when constructing a 3D cockpit you can additionally use this …/cockpit/-PANELS-/Panel.png file - the instruments that X-Plane draws on the 2D panel will also appear in your 3D model.

The …/cockpit/-PANELS-/Panel.png texture doesn't contain any instruments when you load it into Blender (unless you've painted them on yourself). This makes it hard to tell in Blender where X-Plane will draw the instruments. So it's easier if you use a screenshot of the panel with the instruments drawn on it, instead of the real Panel Texture. If your display is larger than your Panel Texture, then this is simple:

* Run PlaneMaker.
* Choose Background → Rendering Options and set the size to be equal to the size of your Panel Texture.
* Restart PlaneMaker
* Choose Standard → Panel
* Take a screenshot: Press Alt PrintScreen (PC) or Command Shift 3 (Mac).
* Paste (PC) or load (Mac) the screenshot into an image editor application.
* Crop the window borders etc from the screenshot so that the image is exactly the same size as your Panel Texture.
* Save the screenshot as ScreenshotPanel.png (or any filename ending in *panel.*) in the same folder as your plane's .acf file.
* Use the ScreenshotPanel.png texture on those faces that you want to display moving cockpit instruments in X-Plane.
* The screenshot file does not need to be distributed with your finished plane.

If your Panel Texture is larger than your display then you cannot take a screenshot of the whole panel. In this case you'll need to take multiple screenshots of the panel in PlaneMaker and stich them together in an image editing application.

If you later want to resize your Panel Texture then use the procedure described below.

Note that X-Plane versions prior to 8.20 only display the 3D cockpit when running at the default 1024x768 resolution. You may want to mention this in the Readme with your plane if your plane is intended to work in X-Plane versions prior to 8.20.

### v9: Cockpit Panel Regions

The cockpit Panel Texture uses a lot of video memory, much of which is wasted when the 3D cockpit is being displayed:

* X-Plane has to round up the height and width of your Panel Texture to be powers of two. eg if your Panel Texture is 1600×1200 pixels then X-Plane rounds this up to 2048×2048 pixels, which requires 16MB of video memory. More if you also supply a LIT Panel Texture.
* Typically up to half of your Panel Texture represents your plane's windscreen, which is fully transparent. You can't make use of this part of the texture in any useful way in a 3D cockpit, so the memory that it consumes is wasted. (Note: You can construct a tinted windscreen in your 3D cockpit quite cheaply by using a small semi-transparent part of the non-panel texture).
* The Panel Texture contains an alpha channel for transparency. The alpha channel accounts for ¼ of the memory that the texture consumes. But often your only need for transparency in the Panel Texture is to represent the 2D windscreen, which is of no use in a 3D cockpit, so the memory that the alpha channel consumes is wasted.

A "Panel Region" is a new texture which is cut out from your Panel Texture:

* You can create up to 4 Panel Regions (which can overlap).
* The height and width of a Panel Region texture must be a power of two eg 128, 256, 512, 1024 or 2048, but it doesn't have to be square.
* Panel Region textures are opaque - they don't contain an alpha channel.

When you use Panel Regions instead of the Panel Texture to texture your 3D cockpit, X-Plane discards the Panel Texture's alpha channel and also discards all areas of the Panel Texture other than the pieces that you cut out to make the Panel Regions. This reduces video memory requirements and improves performance.

#### Creating a Panel Region

* In the UV/Image Editor window, select your Panel Texture from the pop-up menu.
* Choose Image → X-Plane panel regions → Create new region
* Enter the co-ordinates in your Panel Texture where you want the bottom-left pixel of the new Panel Region to start, and the width and height of the new Panel Region.

Any faces that you've textured using the Panel Texture which are contained inside the new Panel Region are transferred over to use the new Panel Region.

Any areas that are fully transparent in the Panel Texture are coloured sky blue in the new Panel Region. You'll get undefined (ie weird) results in X-Plane if you use these sky blue areas to texture your faces.

(Note: When you create a Panel Region, Blender also creates a hidden object named "PanellRegionHandler" to store accounting information. Don't mess with this object).

#### Deleting a Panel Region

* In the UV/Image Editor window, select your Panel Region from the pop-up menu.
* Choose Image → X-Plane panel regions → Delete this region

Any faces that you've textured using this Panel Region are transferred back to using the Panel Texture.

The deleted Panel Region will remain in the UV/Image Editor window's pop-up menu for a while until Blender figures out that it can remove it. But the deleted Panel Region won't count towards your maximum of four Panel Regions.

#### Re-loading the Panel Regions

The Panel Regions aren't automatically updated when you edit your Panel Texture in an image editor application and then reload it in Blender, or when you reload your .blend file.

* In the UV/Image Editor window, select your Panel Texture from the pop-up menu.
* Choose Image → X-Plane panel regions → Reload all regions


### Using Blender to create X-Plane objects

Only Lamps and Meshes are exported to X-Plane. You can use other Blender object types, eg Curves and Surfaces, to construct your scenery as long as you convert them to meshes before exporting to X-Plane.

#### Lamps

Only Lamp objects of type "Lamp" are exported to X-Plane. Lamp objects of types "Area", "Spot", "Semi" and "Hemi" are ignored (and so can be used to illuminate your model in Blender).

**v8/v9**: Lamp objects with certain words in their names have special behaviours when exported to an X-Plane v8 or v9 object:

* _Lamp_ - Normal (legacy) light. The colour is determined by the R,G,B sliders on the Lamp panel (**F5**).
* _Flash_ - Flashing (legacy) light. The colour is determined by the R,G,B sliders on the Lamp panel (**F5**).
* _Traffic, smoke_black, smoke_white_ - As for X-Plane v7 objects; see below. (R,G,B settings are ignored).
* other - X-Plane pre-defined "named" or "custom" light. (Supported by X-Plane 8.50 and later. R,G,B settings are ignored). The name of the X-Plane light is taken from the value of a property named name if this exists, otherwise from the name of the lamp object.

**v7**: Lamp objects with certain words in their names have special behaviours when exported to an X-Plane v7 object:

* _Flash_ - Flashing light. The colour is determined by the R,G,B sliders on the Lamp panel (**F5**).
* _airplane_beacon_ - Red pulsing anti-collision light. (R,G,B settings are ignored).
* _airplane_strobe_ - White strobe light. (R,G,B settings are ignored).
* _Traffic_ - Cycles red, orange, green. (R,G,B settings are ignored).
* _smoke_black_ or _smoke_white_ - Not really a light; emits smoke. The size of the smoke puffs is determined by the Energy slider on the Lamp panel (**F5**) (R,G,B settings are ignored).
* other - Normal light. The colour is determined by the R,G,B sliders on the Lamp panel (**F5**).

**csl**: Lamp objects with certain names have special behaviours when exported to an X-Plane CSL object. The XSquawkBox documentation strongly recommends that you use these special lights:

* _airplane_landing_ - White landing light. (R,G,B settings are ignored).
* _airplane_taxi_ - White taxi light. (R,G,B settings are ignored).
* _airplane_nav_left_ - Red navigation/position light. (R,G,B settings are ignored).
* _airplane_nav_right_ - Green navigation/position light. (R,G,B settings are ignored).
* _airplane_beacon_ - Red pulsing anti-collision light, on when engines are running. (R,G,B settings are ignored).
* _airplane_strobe_ - White strobe light. (R,G,B settings are ignored).
* other - Normal light. The colour is determined by the R,G,B sliders on the Lamp panel (**F5**).

**v8/v9**: Custom lights (supported by X-Plane 8.50 and later) are created using the vertices from a Mesh object:
In the Material buttons panels (**F5**) add a new material to the mesh, then press the Halo button on the Links and Pipeline panel. You should use just one material.

* The Halo button and the R,G,B,A sliders on the Material panel control the light's R,G,B and A values. Alternatively you can create [property](#properties) named _R, G, B_ and/or _A_ to set these values.
* The HaloSize control on the Shaders panel controls the light's S value.
Also press the HaloTex button on this panel to make Blender render the light correctly.

In the Texture buttons panels (**F6**) add a new texture to the material, and change the Texture Type to _Image_. You should use just one texture.

* On the Image panel load the texture file that contains the light that you want to use.
* On the Map Image panel press the UseAlpha button.
Use the MinX, MinX, MaxX, MaxY settings to select a subset of the texture.

To drive the custom light using a dataref add a String [property](#properties) named _name_.

#### Meshes

Create faces with 3 or 4 edges (called "_tri_"s and "_quad_"s in X-Plane).

In the Link and Materials Editing panel (**F9**):

* Set Smooth and Set Solid control whether to smooth edges of faces in a mesh. This is useful when using multiple faces to simulate a curved surface. Go to "Object Mode", select the mesh and press Set Smooth. The effect is only visible in Blender 3D View windows when the Viewport Shading button is set to Solid or Shaded.  
    **v7**: Only faces that are part of a [Strip](#strips) will be smoothed when displayed in X-Plane.

In the Texture Face Editing panel (**F9**) available in UV Face Select mode:

* Tex button controls whether the face has a texture:  
    In an image editor application create one texture file that is like a "[collage](http://en.wikipedia.org/wiki/Collage)" of all of the textures that you need in your model. The height and width of the texture file must be a power of two eg 128, 256, 512, 1024 or 2048 (X-Plane v9 only), but it doesn't have to be square. (See _…/Custom Scenery/KSBD Demo Area/KSBD_example.png_ for an example).
Save the texture file in 32bit or 24bit PNG format (ie with or without an "Alpha" channel) in the aircraft or scenery folder where you want the X-Plane _.obj_ file to end up.
Use the UV/Image Editor window to control mapping of the textures to the face.
* Tiles button controls whether the face is rendered with "polygon offsetting" (_ATTR_poly_os_) in X-Plane. Press this button for faces that lie flat on the ground to prevent Z-buffer thrashing in X-Plane. Don't press this button for other faces. For best results with X-Plane versions prior to 8.50 you should ensure that objects that use polygon offsetting are listed first in your .env or .dsf scenery file.  
    **v7**: "polygon offsetting" does not produce reliable results in X-Plane versions prior to 8.20.  
    **csl**: This button has no effect when exporting CSL objects.  
* Collision button indicates that the face is not "hard" (ie not "landable on") in X-Plane. Making faces hard is very expensive, so this button should normally be pressed. Unpress this button only for things like helicopter landing pads.  
    (Note: The meaning of this button was changed in v1.50. Use [this](http://marginal.org.uk/x-planescenery/collide.txt) script to turn the Collision button back on for all faces).  
    **v9**: You can control whether it is possible to fly under this hard face; add a Bool [property](#properties) named deck and give it the value True. You can't fly under hard faces in X-Plane v8.  
    **v8/v9**: You can specify the surface type; add a String [property](#properties) named _surface_ and give it the value _water, concrete, asphalt, grass, dirt, gravel, lakebed, snow, shoulder_ or _blastpad_. The surface type is ignored by X-Plane versions prior to 8.50.  
    **v7**: Only faces with 4 edges (ie "_quads_") are exported as "hard".  
    **v7**: X-Plane versions prior to 8.20 have a bug where _.obj_ files that contain hard faces must be placed in WorldMaker with an "object heading" of 0. Otherwise the "hard" part of the surface ends up in the wrong place.  
    **csl**: This button has no effect when exporting CSL objects.
*Twoside button controls whether one or both sides of the face are displayed. Unless you have a lot of double-sided faces it is cheaper to avoid this button and to use two single-sided faces back-to-back instead.
* Alpha button is a hint to Blender and to X-Plane that the face is transparent or translucent. Use this for outwards-facing transparent or translucent faces to instruct X-Plane to draw these faces last so that you can see other faces through them. Don't press this button for opaque (normal) faces. See [drawing order](#order) for more fine-grained control over drawing order.

**v8/v9**: In the Material buttons panels (**F5**) you can change the way that the mesh reacts to light by specifying a material. Changing between materials in X-Plane is expensive so you should ensure that you only use a few materials in your model. Press Add New to create a new material, or choose an existing material (if any) from the drop-down list. You should use just one material.
Only a few of Blender's many material buttons affect X-Plane:

* Col button and the R,G,B sliders on the Material panel control the diffuse colour of the faces. X-Plane combines the colours that are specified by the texture (if any) with this setting. The default X-Plane setting is _1, 1, 1_ (white). However the default setting of a new material in Blender is _0.8, 0.8, 0.8._
You should set this to _1, 1, 1_ - control the diffuse colour of the faces by editing the texture file instead.
* Spec slider on the Shaders panel controls the specularity (shininess) of the faces. The default X-Plane setting is 0 (matt). However the default setting of a new material in Blender is 0.5.
* Emit slider on the Shaders panel controls the emissive brightness of the faces. Emissive faces give off light so the effects of this setting are most obvious at night. It is usually cheaper and easy to use __LIT_ textures to control night-time brightness instead of using this setting. However using this setting allows you to create faces that also give off light during the daytime, eg on overcast days, which __LIT_ textures do not. The default X-Plane and Blender setting is 0 (not emissive).
* Mir button and the R,G,B sliders on the Material panel control the emissive colour of the faces.

Use [this](http://marginal.org.uk/x-planescenery/normalise.txt) script if you need to reset all faces in the scene to standard settings (ie no polygon offsetting, not hard, single sided, not transparent).

You can add "modifiers" in the Modifiers panel to change the way that the Mesh appers. Some useful modifiers when modelling for X-Plane are:

* EdgeSplit - automatically sharpen edges between mesh faces (this only has an effect if you've used the Set Smooth button)
* Subsurf - produce a more detailed version of the mesh by subdividing faces
* Curve - bend the mesh along a curved path

#### Lines

Blender doesn't support Lines directly. Use a mesh with one 4-edged face instead. The pair of vertices at each end of the "line" must be within 0.1 units of each other. The face must be the only face in its mesh and must not have a texture assigned to it.

Assign a material to the face and use the Col button and the R,G,B sliders on the Material panel to control the colour of the line. Faces not linked to a material will be exported coloured grey.

### v8/v9: Animation

You can make lamps, meshes and lines animate in X-Plane according to the value of any of the simulator datarefs listed [here](http://www.xsquawkbox.net/xpsdk/docs/DataRefs.html) that have type "int", "float" or "double".

#### Basic animation

Create an "Armature" object. Make the lamps and/or meshes that you want to animate the children of the armature's "bone":

1. Click on the lamps and/or meshes (the "children")
2. Shift-click on the armature
3. **Choose Pose Mode from the Mode menu in the 3D View window's toolbar**
4. Click on the bone (the "parent")
5. Press **Ctrl-P** and select Bone from the popup menu

Once you have assigned a parent bone to your lamps/meshes, you can specify the simulator [dataref](http://www.xsquawkbox.net/xpsdk/docs/DataRefs.html) that will drive the animation:

6. Choose Object Mode from the Mode menu in the 3D View window's toolbar
7. Select the child lamp or mesh
8. From the 3D View window's menubar choose Object → Scripts → X-Plane Animation
9. In the Parent Bone panel, use the pop-up menu to select the [dataref](http://www.xsquawkbox.net/xpsdk/docs/DataRefs.html)
(or you can type in just the "leaf" name of the dataref into the text field, or the full name of a custom dataref)
10. Some datarefs require you to specify a "Part number";
    eg the dataref _sim/flightmodel/engine/ENGN_thro_ represents the engine throttle settings, so you need to specify which engine you're referring to. Specify a "Part number" of _0_ for the first engine, _1_ for the second engine etc
11. Press the Apply button

Use frames to represent the desired position of the lamps/meshes at various dataref values - X-Plane will [interpolate linearly](http://en.wikipedia.org/wiki/Linear_interpolation) between the positions:

1. In the Animation Frame field, in the Buttons window's menubar, select frame 1
2. Click on the armature
3. Choose Pose Mode from the Mode menu in the 3D View window's toolbar
4. Click on a bone
5. Move and/or rotate the bone
6. Press **i** and specify a _LocRot key_ (ie location and rotation)
7. Repeat for any other bones in the armature
8. Select animation frame 2 and repeat

(Note: X-Plane's animation syntax is quite simple; so don't use IPOcurves, Vertex Groups, Deformations, Shape Keys or any other advanced Blender animation techniques since these will be ignored by the exporter - only the positions specified by keys in the first n frames are significant to X-Plane.)

**v8**: X-Plane v8 only supports two frames, so if you want your _.obj_ file to work in X-Plane v8 then you should insert "LocRot" keys only in frames 1 and 2. If you insert keys in frame 3 and above then your animation will not work at all in X-Plane v8. Use the Delete button in the X-Plane Animation dialog to delete any keys from additional frames.

**v9**: You can add "LocRot" keys in as many frames as you like. If you skip a frame then Blender and X-Plane will use the pose from the previous frame.

The X-Plane Animation dialog renames the parent bone to the "leaf" name of the dataref. So pressing the Draw Names button in the Armature panel can be helpful to see what's going on when you have lots of animations.

Use the Action Editor window to get an overview of which bones in the selected armature have keys inserted into which frames.

#### Controlling animation response to dataref values

By default, X-Plane will display the meshes in the frame 1 position when the dataref has a value of 0, and in the last frame position when the dataref has a value of 1. You can change these values:

1. Choose Object Mode from the Mode menu in the 3D View window's toolbar
2. Select the child lamp or mesh
3. From the 3D View window's menubar choose Object → Scripts → X-Plane Animation
4. Specify in the Frame #n fields the dataref values that correspend to each frame;  
    eg the yoke pitch dataref _yolk_pitch_ratio_ takes values between -1 (forward) and +1 (back) in X-Plane. So, to make X-Plane display the position in frame 1 when the yoke is pushed fully forward specify _-1_ in the Frame #1 field
5. Press the Apply button

**v9**: X-Plane will [extrapolate](http://en.wikipedia.org/wiki/Extrapolation) your animation when the dataref has a value outside of the range that you specified in the _Frame #n_ fields. You can stop the extrapolation and "clamp" your animation's position by repeating the poses and _Frame #n_ values in the first two and/or the last two frames. Or you can cause your animation to loop back to frame 1 when the dataref value exceeds a certain number by specifying this number in the _Loop_ field.

#### Using multiple datarefs

You can animate your lamps/meshes using multiple bones, each bone representing a different dataref:

1. In Edit Mode add additional bones to the armature.
2. Still in Edit Mode, in the Armature Bones panel, create parent/child relationships between each bone. (Note: This panel also lets you rename bones. Don't do this - use the X-Plane Animation dialog to name the bones after the datarefs that they represent).
3. Use the technique described [above](#basic_animation) to make your lamps/meshes the children of the "youngest" bone in the chain.
4. Insert _LocRot_ keys for every bone in the chain (each bone can have a different number of keys).

The X-Plane Animation dialog displays the settings for the lamp/mesh's parent bone, gandparent bone etc. (Note: Don't change the parent/child relationships between your lamps/meshes and their parent bones while the X-Plane Animation dialog is being displayed).

#### Hiding lamps and meshes

You can make all of the lamps and meshes in an animation disappear when a dataref is within a certain range:

1. Use the technique described [above](#basic_animation) to make your lamps/meshes the children of an armature bone
(If you don't want to animate your lamps/meshes then don't insert any animation keys for this bone, and the bone doesn't have to be a valid dataref)
Choose Object Mode from the Mode menu in the 3D View window's toolbar
Select a lamp or mesh that you want to hide
From the 3D View window's menubar choose Object → Scripts → X-Plane Animation
In the last panel, press the Add New button
Specify the dataref and the range of values (it's OK to use datarefs that are not otherwise used in the animation)

You can make hidden lamps/meshes re-appear when a dataref value is within a certain range by adding another entry, and changing the type from Hide to Show. The dataref that you use to "show" the animation can be the same or different than the datarefs that you used to "hide" the animation. (The animation is always shown by default, so you only need to use a Show entry if you have used one or more Hide entries and you want to override them).

The order of Hide and Show entries is significant; the animation will be hidden if any of the Hide dataref values are in range, unless a subsequent Show dataref value is also in range. You can use the Up and Down buttons to change the order of the entries.

Note that the Hide and Show entries apply to all children of all bones in the armature. You can make an armature the child of a bone in a different armature; in which case all children are affected by any Hide and Show entries in parent armatures.

v8/v9: Drawing order

The order in which X-Plane draws the animations, lights, lines and triangles in your scenery or cockpit object usually has no effect on the appearance. So the exporter optimises the order of animations, lights, lines and triangles in your object to minimise the number of OpenGL state changes and therefore maximise X-Plane's framerate.

However drawing order does become important if you use transparent and/or translucent textures on some of your faces - transparent and translucent faces must be drawn last, otherwise other faces and lights will not be visible through them. You should therefore tell Blender which faces are transparent/translucent using the Alpha button in the Texture Face Editing panel (F9) in UV Face Select mode. The exporter will ensure that X-Plane draws these faces last.

But sometimes you need even more control over the drawing order - eg modelling a cockpit with a transparent HUD and (obviously) a transparent canopy; the HUD must be drawn after the canopy.

You can specify the relative order in which lamps, meshes etc should be drawn by assigning them to "Groups" on the Object and links panel (F7):

Objects that don't belong to a group are drawn first.
The groups are sorted by alphabetical order, and then
objects that belong to the first group are drawn next.
…
objects that belong to the last group are drawn last.

eg in the case of the cockpit with transparent canopy and HUD, we could put the canopy and HUD into separate groups named GroupA and GroupB respectively. Since A is before B in the alphabet, the canopy would be drawn before the HUD (and both would be drawn after the rest of the cockpit).

To add objects to a new group:

Select the meshes that you want to be drawn late.
Press the Add to Group button on the Object and links panel (F7) (or press Ctrl-G).
Choose ADD NEW.
Give the new group a name.

Objects that belong to a group are highlighted in green instead of pink so that you can easily distinguish them.

v8/v9: Drawing group

You can specify when X-Plane should draw your scenery object relative to other scenery elements:

Add a Blender object of type "Empty" to your scene.
Add a property to the Empty object named group_terrain, group_beaches, group_shoulders, group_taxiways, group_runways, group_markings, group_airports, group_roads, group_objects, group_light_objects or group_cars.
Give the property a value between -1 and -5 to make X-Plane draw your object before this group, 0 to draw your object with this group, or between 1 and 5 to draw your object after this group.

eg to make X-Plane draw your object at the same time that it draws runway markings add a property named group_markings to an Empty object and give it the value 0.

v8/v9: Slung load weight

You can specify the weight of an object for use in X-Plane's physics engine if the object is being carried by a plane or helicopter:

Add a Blender object of type "Empty" to your scene.
Add a property to the Empty object named slung_load_weight and specify the weight in pounds.

Optimising for X-Plane

v7: Strips

As well as basic 3- and 4-edged faces ("tri"s and "quad"s), X-Plane v7 objects support two compound types - "tri_fan" and "quad_strip". These are strips of two or more tris and quads that share common edges. Because the faces in these strips share common edges, X-Plane and the underlying OpenGL renderer have a third or a half as much work to do to render them compared to individual tris and quads. This gives higher frame rates.

In order for a pair of faces to be considered for inclusion in one of these strips, the following conditions need to be true:

The faces must be facing the same way.
Each pair of faces must share a common edge (apart from the first and last face).
Each shared edge must have the same texture co-ordinates in both faces.

In practice this means that the texture must be reversed in alternate faces in the strip. In the case of tris this can also be achieved by mapping a single area of the texture across all the tris, with the tip of the tris at the centre of the texture area. Use UVs → Copy & Paste from the UV/Image Editor window to automate the creation of strips.

These compound types aren't supported directly by Blender. However, the export script automatically tries to spot when it can use them.

v8, v9 & csl: The performance gains from using strips are more modest in X-Plane v8 and v9, and for CSL objects. These compound types aren't supported in v8/v9 objects (X-Plane v8 and v9 use more advanced techniques) and the only saving from using strips over some other UV mapping methods is in reduced "vertex count". It probably isn't worth going out of your way to look for opportunities of making strips.

Level Of Detail

X-Plane has borrowed the concept of "Level Of Detail" from 3D games. This works on the principle that when you're viewing an object from a large distance it can be displayed with reduced detail without you noticing the difference. By displaying distant objects with reduced detail we can simulate a more complex scene than would be possible if all objects were drawn at maximum detail.

Use Layers to draw scenery and CSLs (but not aircraft Cockpits or Misc Objects) with multiple Levels Of Detail. Objects in layers 1-3 are visible in X-Plane at the following distances:

Layer

Distance

1

< 1000m

2

1000-4000m

3

4000m-10000m

Changing the texture size

If you run out of space in your texture file then you can increase the size. The panel texture can by 1024×any size in X-Plane v8, and any size up to 2048×2048 in X-Plane v9. The height and width of a non-panel texture file must be a power of two eg 128, 256, 512, 1024 or 2048 (X-Plane v9 only), but it doesn't have to be square.

You should use the following procedure to ensure that your UV mappings and/or PlaneMaker instrument layouts are preserved:

Create a new, larger, texture in an image editor application.
Panel texture: Paste the original texture into the lower left corner of the new texture.
Non-panel texture: Paste the original texture into one of the corners of the new texture, or aligned on a multiple of the original texture's width and height.
In Blender, in the UV/Image Editor window, select the original texture from the pop-up menu.
Choose Image → Replace and fixup UV mapping…
Select the new image and press Replace image.
In the Fixup UV mapping dialog, press the button in the cluster of buttons that represents where you placed the original texture in the new texture.

You can also use this technique if you want to combine 3D models that use different texture files; paste all of the textures used by the 3D models into a single new texture file, then use Image → Replace and fixup UV mapping… on each of the original textures.

Blender tips

Blender has a quirky user interface:

By default, Right mouse button does what you would expect Left mouse button to do. I strongly recommend that you change this; drag down the top menubar to reveal the User Preferences window, select the View & Controls tab and choose Select with: Left Mouse. See this tutorial for a fuller explanation.
Space does what you might expect Right mouse button to do.
The user interface is "modal". Buttons and keys do different things depending on whether you are in "Object", "Edit", "UV Face Select" or "Pose" mode. (And I thought modal UIs went out with "vi"). Tab changes mode.

Auto-saving

Blender can automatically archive old copies of your .blend files when you save. This is useful if you later want to revert to an older version. In the User Preferences window, on the Auto Save tab, choose the number of Save Versions. The older versions of your file will be called .blend1, .blend2 etc.

Blender can also periodically save a copy of your work in case Blender or your computer crashes, or in case you quit Blender without saving. On the Auto Save tab press Auto Save Temp Files. Also, on the File Paths tab, ensure that Temp is set to a folder that exists on your machine. This is where the auto-saved files will be created. (The default value of /tmp is fine for Mac and Linux, but /tmp doesn't exist on most Windows machines so you should change this setting).

Properties

"Properties" are used to specify animation parameters, "named" lights and the drawing group. You can see an object's properties by selecting it and pressing F4 to display the Logic panel. Press the Add Property to create a new property.

Each property has three fields; Type, Name and Value. If you want to supply a non-numeric value, eg the name of a "named" light, you'll first need to change the Type from Float to String.

Limitations

Import object

smoke_black and smoke_white X-Plane primitives are ignored.
ambient, blend and specular attributes are ignored.
The importer usually can't work out which faces are partially or wholly transparent. You should tell Blender which faces are transparent using the Alpha button in UV Face Select mode after import.

Import plane

Importing planes made with PlaneMaker 7.30 or earlier is not supported. Convert an older plane to v7 by opening it in PlaneMaker 7.63 and re-saving it.
Wings are simplified to reduce polygon count. Any wing curvature (ie the customize chords option in PlaneMaker) is ignored.
Adjacent wing segments may not be exactly joined-up. If not corrected manually this can create shadow effects in XSquawkBox and X-IvAp.
Cockpit objects are ignored. You can use File → Import → X-Plane Object to import cockpits.
Planes (and their weapons, misc objects and cockpit objects) use multiple texture files. These are not automagically merged into one file during the import.
The importer can't work out which faces are partially or wholly transparent. You should tell Blender which faces are transparent by pressing the Alpha button in UV Face Select mode after import.
LOD algorithm can be insufficiently aggressive in layer 2.

Export object

Only Lamps and Mesh Faces (including "lines") are exported.
All faces must share a single texture file apart from cockpit panel faces which can additionally use the cockpit panel texture (this is a limitation of the X-Plane .obj file formats). You can use Image → Consolidate into one image to merge multiple texture files into one file.

Problems

Please email any questions, problems etc to danklaue. If reporting a problem, please:

First, check that you are using the latest version of the scripts.
Try to send me the the .obj, .acf or .blend file (where relevant) and the contents of the Console window. (In Mac OS X, this is the "Console" program. In Windows this the window titled "Blender" that looks like a Command Prompt).

License

These tools are licensed under the Creative Commons Attribution-Noncommercial-ShareAlike license.

Use of these tools does not impose any requirement on you to license your work under a Creative Commons license. For the avoidance of doubt, this means that you can license any scenery that you make using these tools under commercial terms (subject to any licensing restrictions on any imported or library objects that you use).

The team that is carrying on the development and upkeep of this script would appreciate a donation for the time and efforts spent on this script. Although you are under no obligation to do so, it would help in keeping the team motivated to continue updating and improving the script. If you wish to contribute, please click here to donate an amount of your choice via PayPal.