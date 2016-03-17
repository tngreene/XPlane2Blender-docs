# Installation - Detailed Notes

## Download Blender App
Go to
https://www.blender.org/download/

download .zip for OS X or .msi for Windows

OSX:
    unzip downloaded zip file.
    Copy entire unzipped folder into "Applications"

## Set up Blender for scripts
1. In the Blender folder, create a folder named "scripts"
2. In that folder, make another folder named "addons"
2. Launch Blender
2. Pick File -> User Preferences
3. Go to "File" tab in preferences dialog box.
4. Click the folder icon next to the line that says scripts.
5. Navigate to your scripts folder.
6. When done you should see something like /Applications/blender-2.76b-OSX_10.6-x86_64/scripts/ in the line.
7. Click "save user settings"
8. Close the preferences dialog box.
9. Quit Blender

Power user note: the scripts folder can be anywhere on your hard drive and have any name.  However, the "addons" folder within scripts *must* be named addons all lower-case, no spaces.

## Installing X-Plane2blender
1. Download the latest version of X-Plane2Blender. **Open Issue: where do we download it from?  This link needs to be finalized.**
2. Unzip the download.
3. Move the io_xplane2blender _into_ your "addons" folder you created.
4. Start Blender.
5. Pick File->User Preferences
6. Go to the "Add-Ons" tab
7. Type "xplane" into the search field (no hyphen).  You will see only one add-on: Import-Export: Import/Export: X-Plane
8. Check the checkbox next to the icon of the dancing person on the right.  The exporter is now enabled.
9. Click "save user settings".
10. Close the preferences dialog box.

## Customizing Blender
### Preferences to change
From File->Preferences, a few settings I like to customize to make Blender easier to use:
- Interface Tab: check "Zoom To Mouse Position."  This lets you zoom in and out of the thing you are pointing at.
- Input: select with: pick left.  
### Cleaning out the Startup Configuration
Blender has a "startup file" - a file that is loaded every time you ask for a new blank canvas.  By default it has a light, a cube, and a camera. I find that annoying and always have to delete them to get going.  We can _permanently_ delete them by:
1. For each item in the scene, right-click it in the outliner and pick "delete".
2. Pick File -> Save Startu File

Blender will do something you have never seen before: it will create a tiny popup menu under your mouse that says: Ok? Save Startup File

- If you click "Save Startup File" the operation is confirmed and the save happens.
- If you move the mouse away, the operation is canceled.

This kind of "menu-based confirm" is all over Blender.  It is tricky to get used to at first, but can be very fast when working.

### Customizing the Screen
Blender has a huge number of screens and lots of options to customize how the screen is organized.

Blender's default layout is good for general modeling, but I'm not a fan of the default UV editing view.  Here'es how to customize the view for texturing:
1. Start Blender.
2. If you are not already in the "default" screen layout, pick that.
3. Click the + sign next to the screen layout menu.  A new item Default.001 appears.
4. Rename it to "texturing"
5. Put the mouse over the divide between the 3-d window and the main menu bar.  A horizontal pair of arrows will appear.
6. Right click and pick "split area" - a vertical line appears.  
7. Move the mouse to put the line about at the midpoint of the main window and click.
8. There are now two main editing areas.
9. In the lower left corner of the right side window there is an icon with a cube and up-and-down arrows.  Pick it and select "UV/image editor"
10. Put the main screen layout back to default.
11. Pick file->save user startup file to save this change for future documents.