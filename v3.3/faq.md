# FAQ

- [In my X-Plane layer I've pointed to the right texture, but the exported object contains a wrong texture path like "/././././...texture.png".](#in-my-x-plane-layer-ive-pointed-to-the-right-texture-but-the-exported-object-contains-a-wrong-texture-path-like-texturepng)
- [I have a mesh that is transparent (glass). To correctly display it, it must be drawn at last. That means it needs to be written last in the OBJ file.](#i-have-a-mesh-that-is-transparent-glass-to-correctly-display-it-it-must-be-drawn-at-last-that-means-it-needs-to-be-written-last-in-the-obj-file)
- [How do I add cockpit regions?](#how-do-i-add-cockpit-regions)
- [XPlane2Blender does not support feature X from the OBJ-file format specification and I need to write my _hacks_ into the OBJ-file after every export.](#xplane2blender-does-not-support-feature-x-from-the-obj-file-format-specification-and-i-need-to-write-my-hacks-into-the-obj-file-after-every-export)
- [I've assigned a texture to my materials but I can't see it in Plane-Maker or X-Plane.](#ive-assigned-a-texture-to-my-materials-but-i-cant-see-it-in-plane-maker-or-x-plane)
- [I have an aileron/rudder/... that need's to be rotated along an arbitary axis. How can I do that?](#i-have-an-aileronrudder-that-needs-to-be-rotated-along-an-arbitary-axis-how-can-i-do-that)
- [How can I quickly see if my animation exported correctly?](#how-can-i-quickly-see-if-my-animation-exported-correctly)
- [I've opened files created with an older version of XPlane2Blender and now (all) manipulators have the wrong type.](#ive-opened-files-created-with-an-older-version-of-xplane2blender-and-now-all-manipulators-have-the-wrong-type)
- [My objects look very dark when brought into X-Plane.](#my-objects-look-very-dark-when-brought-into-x-plane)


### In my X-Plane layer I've pointed to the right texture, but the exported object contains a wrong texture path like "/././././...texture.png".

This is an issue with older versions of XPlane2Blender. Be sure to uncheck "Relative Paths" when choosing the texture file. XPlane2Blender was only capable to resolve **absolute** file paths back then.

### I have a mesh that is transparent (glass). To correctly display it, it must be drawn at last. That means it needs to be written last in the OBJ file.

You can override the _weight_ of each object, material or bone. The _heavier_ it is, the farer to the end of the OBJ-file it drops. Glass objects however should be within theire own OBJ-file and marked as "glass" in Plane-Maker.

### How do I add cockpit regions?

Simply said, don't do that. It is deprecated.

### XPlane2Blender does not support feature X from the OBJ-file format specification and I need to write my _hacks_ into the OBJ-file after every export.

You can attach any attribute to any object (including lights and bones and also materials) within Blender under X-Plane > Custom Attributes. This will save you from writing those into the exported obj file every time.

### I've assigned a texture to my materials but I can't see it in Plane-Maker or X-Plane.

You have to choose your textures from within the X-Plane layer settings under Scene > XPlane. Textures assigned to materials are not taken into account. Also be sure to UV-unwrap your objects. Generated UV-coordinates are not exported.

### I have an aileron/rudder/... that need's to be rotated along an arbitary axis. How can I do that?

Create an armature with a single bone, then edit the bones position to match the axis. Then parent the object to the bone (not the armature), animate the bone in pose mode and do not forgett to give it a dataref and your object will be rotated along the bones axis.

### How can I quickly see if my animation exported correctly?

Planemaker shows all animations, no matter if the dataref exists or not. This is a good way of testing if an animation looks right or got exported at all. However choosing the correct dataref is another thing.

### I've opened files created with an older version of XPlane2Blender and now (all) manipulators have the wrong type.

If you created your files with the version 3.20.6 [use this script](https://gist.github.com/der-On/739ab883a24ae9cc2c3e) to fix your manipulators.

If you've created your files with a version older then 3.20.6 [use this script](https://gist.github.com/der-On/5480130) to fix your manipulators.

Usage: select the objects with the wrong manipulator type and then run the script within blender's text-editor.

### My objects look very dark when brought into X-Plane.

In the Material tab, set the diffuse intensity of the material to 1.0 and the diffuse color to a full white.
For X-Plane the diffuse color will be multiplied with the intesity and the resulting diffuse color will be multiplied with the texture color. 

Example: a red diffuse color of R = 1.0, G = 0.0, B = 0.0 with an intensity of 0.8 will result in a X-Plane material color of R = 0.8, G = 0.0 and B = 0.0. A fully white pixel in the texture will then appear in exactly this color.

This behaviour is however usefull to create colored variations of objects using the same texture.

Also check that the "Emit" value under "Shading" is set to 0.0 to not make the object "glow" in X-Plane.

*Note to Cycles*: If you're using Cycles to bake the textures, don't forget to switch back to "Blender Render" and assign non-cycles materials to all the objects.

If you think this is a good thing [buy me a beer](../../Donations).