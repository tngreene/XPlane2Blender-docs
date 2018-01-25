# Aiming Special Non-WYSIWYG Lights

In XPlane2Blender 3.4, a certain type of "WYSIWYG" light was added:

> If the Lamp is a "Spot" (or other non-"Point") lamp **and** a "Named" or "Param" type **and** the light name is included in the ``lights.txt`` file:
> - XPlane2Blender will export the Lamp's rotation with What-You-See-Is-What-You-Get behavior
> - The exporter uses Blender's rotation, even if a param list includes X, Y, Z or DX, DY, DZ components. (The param list must still be valid.)

This means "Custom" lights, unknown light names, and point lights cannot simply use their Blender rotation value to aim the light and an advanced hack must be used instead. While previous versions of this trick have been developed, new optimizations have broken some methods. **It is very unlikely that this trick applies to your project.** "Custom" lights are a discouraged (but not deprecated) feature; ``lights.txt`` will always be updated and should **never** be edited manually; and, since billboard lights rarely need **aiming** at all, it is far simpler to use a param light to [change the directionality of a billboard](https://developer.x-plane.com/?article=airplane-parameterized-light-guide#Directionality_of_Lights) than using this trick.

## The "Useless Keyframe" Trick
After creating your Lamp, make an animation on it with the following details:

> 1. Dataref: "none" (or another non-existent dataref)
> 2. Rotation Keyframe 1: Whatever angle you want to aim the light at, a value of 0 for the dataref
> 3. Rotation Keyframe 2: A different angle than Keyframe 1's angle, a different value than Keyframe 1's value

## How It Works
1. X-Plane selects which frame of an animation to interpolate to based on the value of the dataref associated with it. Since "none" is not a real dataref, its value will always be 0
2. Therefore, the animation will always be stuck on Keyframe 1, light pointing in the direction you want it to
3. Keyframe 2 exists and has "different rotation value/dataref value" pattern because:
    - An animation must have more than one keyframe or the exporter will not include it in the OBJ
    - An animation where all keyframes have the same rotation will make the exporter not include it in the OBJ 
    - All dataref values in an animation must be different or X-Plane considers it invalid with potentially unintended results

The "Useless Keyframe" Trick represents the simplest and safest way to meet the above requirements.

If you have a several of these special lights that are aiming in the same direction, you can save time and group them together. Parent all of them to an Empty or Bone, and apply the "Useless Keyframe" trick to only the parent.
