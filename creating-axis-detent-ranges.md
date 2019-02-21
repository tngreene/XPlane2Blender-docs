# Creating Axis Detent Ranges {#defining-axis-detent-ranges}

## Definition {#definition}

| Concept | Definition |
| :--- | :--- |
| Drag Axis Animation | The main animation in a Drag Axis With Detents manipulator |
| Drag Rotate Animation | The main animation in a Drag Rotate With Detents manipulator |
| Detent Animation | The animation controlling the detent action |

These are made with either Blender Location or Rotation keyframes.

| Concept | Definition |
| :--- | :--- |
| Dataref 1 Keyframes | The dataref values and path used with the Drag Axis or Drag Rotate Animation |
| Dataref 2 Keyframes | The dataref values and path used with the Detent Animation |
| Detent Keyframes | See `Dataref 2 Keyframes` |

These are made with X-Plane Keyframes. Their minimum and maximum do not have to be the real limits of a Dataref as defined in DataRefs.txt or a custom plugin.

| Concept | Definition |
| :--- | :--- |
| Maximum Drag Height | The maximum a detent stick can move from its origin \(in meters\) |
| Axis Detent Range | A way of specifying the minimum height the manipulator must be at to move into the next section |
| Range Start and End | Defines the sub-range of Dataref 1 this range covers, its ends are inclusive |
| Range Height | The height of this section, between 0 and the maximum drag height |
| Axis Detent Ranges table | All Axis Detent Ranges for this manipulator, with one or more ranges |
| Plateaus and Valleys | Using ranges, you can make a description of the physical device you are simulating. This looks like a 2D cross section of "terrain", plateaus and valleys to move along and over. |
| Pits | A range whose start and end are equal, and whose height is less than both its neighbors traps a user who is sliding the control instead of lifting it - without creating a real valley of any width |

With Axis Detent Ranges you are able to simulate a range of cockpit controls like never before!

**Download a complete and working Throttle Quadrant With Detents example: **[AxisDetentRangeTutorial](https://github.com/der-On/XPlane2Blender/files/2886941/axis_detent_range_tutorial.zip)

Here is a rough chart showing our throttle quadrant from the example file.

![](/assets/axis_detent_ranges_in_charts.png "Graphics showing the relationship between the mesh, animations, and ranges")

**The tiny thin line for the range **`.75, .75, 0`** is showing where the pit it. The 1 pixel of whitespace is for illustrative purposes only.**

As you can see, because the Blender Animations, X-Plane Dataref Keyframes, and Axis Detent Ranges are all enforced to be synchronized, the graph minimum heights reflects the real object, whether you're looking at Datarefs or Blender Animations! This is no coincidence! \(Unfortunately you'll have to use your imagination for the OBJ as the model is a plain cylinder and rectangular cube.\)

Once you understand the concept, the rules for what is a valid Axis Detent Ranges table will hopefully be very straight forward.

# Rules For Valid Axis Detent Ranges {#rules-for-valid-axis-detent-ranges}

## General Rules {#general-rules}

Some rules may not be applicable or may seem pedantic if you only have one range, but it is allowed!

* Axis Detent Ranges are only available for Detent related manipulators
* Manipulators with detents must have 1 or more Axis Detent Ranges
* The smart manipulator itself must be valid before Axis Detent Ranges will be checked
* The Dataref Keyframes have only one requirement: the minimum value must be less than the maximum. The whole range of values as defined in DataRefs.txt or a custom plugin do not need to be used. For example: 
  `sim/cockpit2/engine/actuators/throttle_ratio_all`
   real range is 0.0 to 1.0, but we can animate and use only `0.25` to `0.75` or `0.0` to `0.9` as in the example.

## Range Start And End Rules {#range-start-and-end-rules}

Start and End refer to the start and end of a sub range of Dataref 1.

* A range's start must be **less than or equal** to its end
* The start of the **1st** Axis Detent Range must be Dataref 1's minimum, the end of the **last** Axis Detent Range must be Dataref 1's maximum. Every other range's start must be the end of another

With these rules, the starts and ends of the Axis Detent Ranges table covers the full spectrum of Dataref 1 without any gaps or overlaps between ranges, in ascending order

## Detent Dataref And Drag Height Rules {#detent-dataref-and-drag-height-rules}

* The maximum height is determined by the distanced traveled in the Detent Animation
* Values for Height must be between 0 and maximum height
* The Detent Dataref range must not start or end with a negative number.

## Stop Pits {#stop-pits}

* A stop pit is defined as a Range who's start and end are the same, giving it a width of 0. Its height must be less than each of it's neighbors, though 0 is commonly used
* A pit can be the first or last detent range, but never the only one
* Stop **pegs**, where height is equal to or greater than it's neighbor's height, are never allowed



