# Animations

Animations in X-Plane are all driven by datarefs. The numeric value a dataref currently has will be lineary mapped on a previously defined animation sequence.

For example if you animate your yoke from back to forth you must bind this animation to the dataref *sim/joystick/yoke_pitch_ratio* which can have values from -1.0 (yoke full forward) and 1.0 (yoke full backward). Your animation-to-dataref-binding has to take this into account and map the keyframe for the yoke fully backward and fully forward to the corresponding dataref values of -1.0 and 1.0.

## Exportable animations

You **can** only export **Object and Bone** animations for **location and rotation**.
You **cannot export scale** animation.

## Object animation

To export an objects animation:

If the object is not yet animated, animate it. You can animate the object in any way, not just with keyframes.

1. Go to the **XPlane** tab in the Object-Properties.
2. Under *Datarefs* hit **Add dataref** to add a new dataref binding.<br/>
  ![](images/docs-3.2x-animations_1.png)
3. Enter the **Path** to the dataref. If you don't know the path hit **Search dataref**. This will open your browser with a dataref search page.<br/>
  ![](images/docs-3.2x-animations_2.png)<br/>
  If the object is not yet animated animate it now and continue with the next steps.
4. Go to a frame you want to export as a keyframe to X-Plane.
5. Now enter the **Value** of the dataref and hit the **key-icon** next to the Value-input to create a dataref-keyframe. The dataref value will turn green indicating a keyframe. When the dataref in X-Plane reaches this value, the animation will be exactly at this keyframe.<br/>
  ![](images/docs-3.2x-animations_3.png)
6. Go to the next frame you want to export.
7. Enter another **Value** of the dataref and hit the key-icon again to create another dataref-keyframe. The dataref value will turn green again and yellow in all frames between two dataref-keyframes. The animation of the object will now be interpolated between these two keyframes. 
8. Repeat step 5 for each frame you want to export.
9. If your animation only contains location changes change it's type to "Loc" under **Animation**, if it only contains rotation change it to **Rot**. If it contains both keep it at "LocRot". If it is a hide/show animation [see "Show / Hide animations" below](./docs-3.2x-Animations#show--hide-animations).<br/>
  ![](images/docs-3.2x-animations_4.png)

## Bone animation

**Important:** Before parenting the Bone to the Object you want to animate, make sure you applied ***Rotation & Scale*** both to the Object and the Armature (in Object mode)!
![](images/docs-3.2x-animations_4_5.png)<br/>

Animating bones is working almost the same as animating objects.
The only difference is that you have to switch to the **Bone-Properties** while in **Pose-Mode** and there you can add datarefs to the Bone.

![](images/docs-3.2x-animations_5.png)<br/>
![](images/docs-3.2x-animations_6.png)

**Note:** The key-framed dataref value does not get colored yellow or green as with object-datarefs.
This is due to a long lasting Blender bug.

**Attention:** If you add Datarefs in the Object-Properties you will actually be animating the **Armature** Object which holds the bones.

## Gotchas

Animation export can become wacky in some special cases:

1. Rotations larger or equal to 180° will mostly lead to a rotation below 180°.    
    To prevent this insert another keyframe at 90° for example.
2. Rotations along an arbitary axis (not the global X,Y or Z axis) can look flipped.    
    There is no real solution to this problem which exists since the first release of XPlane2Blender 3.20.
    Sometimes it's helpfull to "nest" the problematic object into another animated object.
3. Nested animations only work if every object in the nesting chain is animated as described in "Object animations".
4. Smooth animations in Blender appear clunky or robotic in X-Plane.    
   Blender by default uses Bezier-Curves to interpolate animation between keyframes. X-Plane uses linear-interpolation. To make the animation look smoother in X-Plane you need to add additional dataref-keyframes. However you will never reach the same smoothness as in Blender even when you keyframe every frame.
5. Animation keyframes should always start on the first frame, with the dataref value 0, otherwise animation can end up unwanted positions/result
6. Rotations with negative degrees in the keyframes that go above 180° along the global Y-Axis can start turning in the wrong direction. As a workaround for this bug try to avoid negative rotations above 180° by setting the objects axis in such a way that the rotation can become positive again.

## Show / Hide animations

If you set the **Animation**-type of a Dataref to "Show" or "Hide" the object will be showed or hidden when the dataref reaches a certain value. Show/Hide Animations do not need the object to be animated.

Show/Hide animations require two values. The show or hide will take effect between these two values.

You'll mostly need the dataref twice to make it appear and disappear correctly.
For example if your dataref value ranges from 0.0 to 1.0 and you want your object to be hidden at 0.0 and visible at 1.0 you need to add the dataref twice. The first one needs a "Hide" animation with it's first value 0.0 and second value 1.0. The second dataref needs a "Show" animation with it's first value 1.0 and second value 1.0 or higher.

If you think this is a good thing [buy me a beer](../../Donations).