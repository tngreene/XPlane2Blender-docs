# Lamp Settings
The majority of light authoring in X-Plane is made through its large library of named and parameterized lights. These **"known"** Laminar Research lights come with an assortment of colors, directionality, and tie-ins with datarefs and airplane electrical systems to fit most artistic visions. Fully customizable lights are also available for your artist and complex plugin needs.

These "known" lights are listed in a file called "lights.txt", located in your X-Plane installation folder. A copy is also included in the addon folder "io_xplane2blender/resources/lights.txt". See the section **About lights.txt** for more about using this file. 

## Relevant Blender Settings
### Lamp Type
``Type`` - XPlane2Blender uses this to tell if the artist wants a "Point" or non-"Point" (such as a "Spot") light. "Point" lights have no meaningful direction and are therefore used for things like car headlights and blinking runway lights. They're more optimizable than non-"Point" spotlights. A "Spot" type has a meaningful direction to it and are good for representing things like spotlights. Further mentions of ``Type`` will refer to XPlane2Blender's setting unless otherwise noted.

``Color`` - Custom Lights and old style lights use this for their RGB value

## XPlane2Blender Settings
### X-Plane Light Types
X-Plane's light ``Type`` refers to what type of information is required to use them.

- "Named" - Named lights use a specified pre-made light in X-Plane. They're the most common kind of light authors use
- "Param" - Param lights are like named lights, but also allow partial customization of their behavior such as color, direction, or brightness
- "Custom" - Custom lights are a textured billboards that use a size, a subsection of the OBJ texture, and, optionally, a dataref to control the look of them

"Default (deprecated)", "Flashing (deprecated)", "Pulsing (deprecated)", "Strobe (deprecated)", and "Traffic (deprecated)" are old X-Plane 7 lights, now deprecated.

#### Further Reading
Developer Blog Articles
- [Airplane Parameterized Light Guide](https://developer.x-plane.com/?article=airplane-parameterized-light-guide)
- [Billboard and Spill Lights for OBJS](https://developer.x-plane.com/?article=billboard-and-spill-lights-for-objs)
- [Custom Lights](https://developer.x-plane.com/?article=custom-lights)

OBJ8 Spec Sections
- [GEOMETRY_COMMANDS](https://developer.x-plane.com/?article=obj8-file-format-specification#GEOMETRY_COMMANDS)

Forum Posts
- [Parsed contents of lights.txt](https://forums.x-plane.org/index.php?/forums/topic/133677-parsed-contents-of-lightstxt/)

lights.txt Comment Sections
- Lines 12-18, 38-62, 76-97

### Common Settings
Setting | Default | Description | Requires
------- | ------- | ----------- | --------
``Type``| "Named" | The X-Plane light type, not to be confused with Blender's Lamp ``Type``. See the above "X-Plane Light Types" section for more details |
``Name``| ""      | The name of the light. It should match a "known" Laminar Research light| ``Type`` must be "Named" or "Param"|
``Params``|""     | The numerical parameters for the parameterized light, separated by 1 or more spaces. Comments should start with a "#" or "//" | ``Type`` must be "Param"

### Custom Light Settings
Setting | Default | Description | Requires
------- | ------- | ----------- | --------
``Size``| 1.00    | The size of the custom light, the large the bigger. It isn't in meters or feet, it must be experimented with | ``Type`` must be "Custom"
``Texture Coordinates``| (0.0,0.0,1.0,1.0)| An area of the OBJ's texture where the texture for the light is, specified as a fraction of the textures image between 0.0 and 1.0. The numbers represent the left, top, right, and bottom, respectively | ``Type`` must be "Custom"
``Dataref``|""|An optional dataref that will change the behavior of the light | ``Type`` must be "Custom"
``Enable RGB Override``| Off | When enabled, RGB Override Values will be used instead of the Blender color picker. Useful for certain datarefs| ``Type`` must be "Custom"
``RGB Override Values``| (0.0,0.0,0.0) | The values that will be used instead of the RGB picker | ``Enable RGB Override`` must be on

## About lights.txt
lights.txt is essentially a massive table of information for X-Plane defining lights to be used in the sim. An artist only needs to be concerned with an extremely small portion of it. To read it, you'll need a good text editor (not Notepad or Word!) that can handle different line endings and has an adjustable tabstop (8 seems to work). Comments are prefixed with a #.

**Do not make changes to this file! It may break X-Plane or be erased with the next version of X-Plane.**

The vast majority of this file is not relevant and may be misleading. The most important column is the second one: the light name. Multiple lines with the same light name represent different light drawing styles X-Plane can choose from, not different lights with the same name.

### Anatomy of Param Lights
``
1.                  2.                          3.  4.
LIGHT_PARAM_DEF     appron_light_billboard      5   X Y Z W S
``
1. "LIGHT_PARAM_DEF" declares that the following is a description of a parameterized light 
2. The light name
3. The number of parameters, meaningless to an artist
4. The parameters for this param light which must be replaced by the artist

Any light that doesn't have an associated LIGHT_PARAM_DEF is known simply as a "Named Light".

### Hints For Finding Light Use
Though mostly undocumented, one can usually find the purpose of each light using some of these tips
- Light names are usually very descriptive
- Comments nearby may explain their purpose
- If it is a param light, the parameter names may be of help
- If a light name ends in "_sp" it usually means it's meant to be used as a pair with another light such as "taxi_g" and "taxi_g_sp" or "radio_const_bb" and "radio_const_sp"
- If your file browser is sufficiently advanced, you can search for example uses of the light name in the text of existing .obj files in your X-Plane folder
- If you find an OBJ with a light you're curious about, view it in X-Plane
