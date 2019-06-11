# Empty Settings
Empties have a special usage in XPlane2Blender. Having no mesh and no material, they are a fast and easy way to group and animate other Blender Objects. Post 3.5, they are also the way to specify special types of objects, such as particle emitters. Being a Blender Object, they share all the characteristics with what is covered [here]('35_object_settings.md').

## XPlane2Blender Settings

Empty Special Type

Type | Use
---|---
``None``| No special usage
``Particle Emitter`` | Empties location and rotation will be used to emit particles in X-Plane
``Sound Emitter`` | A planned but unimplemented feature to set X-Plane sound emitters
``Magnet`` | Defines where on a yoke the VR tablet can be attached

### Particle Emitter Settings

``Emitter Name`` - A name from a .pss file that will be reference by the OBJ
``Emitter Index`` - The index of that Emitter Name to use, if there is one. Leave as 0 if not specified.

### Magnet Settings

``Debug Name`` - The human readable name shown for debugging purposes
``Magnet Type`` - Must be one or both of "xpad" or "flashlight"

