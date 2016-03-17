# Advanced Techniques

#### Some tips for render baking

- mirror reflections work best if you set Fresnel to 0.0 and the Reflectivity higher then you would in a regular render
- for better outer reflections add an image texture containing an environment map containing a simple sky and ground and set its mapping to **Reflection**, its influence to **Color** and the Blend to **Screen**.
- render baking is way slower then regular rendering, so try to avoid the expensive mirror reflections with a gloss amount lower then 1.0
- render baking does not use anti-aliasing! That's why you need higher sample rates for ambient occlusion, Area-Lights, Ray-traced soft shadows and things like mirror reflections. It's best to post-process the render baked images with a image-based antialising in your Image-Editor to reduce noise in the texture and to be able to reduce sample rates during render baking.