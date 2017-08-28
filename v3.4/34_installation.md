# Installation

## Download and Install Blender
Go to [the Blender home page](https://www.blender.org/download/) and download the latest version of Blender for your OS. (Note for Windows: If one would like to use multiple versions of Blender on the same computer, use the "portable" .zip version instead of the Windows Installer (.msi) version.)

### OSX:
	- Unzip downloaded zip file.
	- Copy entire unzipped folder into "Applications"

### Windows:
	- Run the Windows Installer (.msi) and follow the prompts
	- If using the .zip version unzip it to an easy to access location

#### Official Blender Documentation
- Installing on [macOS](https://docs.blender.org/manual/en/dev/getting_started/installing/macos.html)
- Installing on [Windows](https://docs.blender.org/manual/en/dev/getting_started/installing/windows.html)
- Installing on [Linux](https://docs.blender.org/manual/en/dev/getting_started/installing/linux.html)

## Download and Install XPlane2Blender
### Automatic Installation
1. Download XPlane2Blender's latest [version](version_url) and put it in a convenient place
2. Launch Blender and open "User Preferences" (**File->User Preferences**)
3. Select the "Add-ons" tab
4. Click the button at the bottom that says "Install from File..."
5. Use the Blender file picker to locate and pick the downloaded XPlane2Blender .zip
6. Click the checkmark next to the words "Import-Export: Export: X-Plane (.obj)". This will enabled the addon
7. Click "Save User Settings" and exit the Window 

### Manual (Advanced) Installation
Blender recognizes that XPlane2Blender is an addon because of some files inside the folder 'io_xplane2blender' which is inside the zip file and because it gets placed into a special "addons" folder.
You can manually install XPlane2Blender by dragging that unzipped ``io_xplane2blender`` folder into it, however it may be up to you to create the folder structure *exactly* by hand.

It is typically located (or should be located) in the following places
- macOS: ``/Users/$USER/Library/Application Support/Blender/2.78/scripts/addons``
- Windows: ``%USERPROFILE%\AppData\Roaming\Blender Foundation\Blender\2.78\``
- Linux: ``$HOME/.config/blender/2.78/``

You can change the location of the scripts folder in User Preferences, however this could affect other addons. Proceed with caution.

#### Official Blender Documentation
- [Configuring Directories](https://docs.blender.org/manual/en/dev/getting_started/installing/configuration/directories.html)

## Customizing Blender
### Preferences to change
From File->Preferences, a few settings I like to customize to make Blender easier to use:
- Interface Tab: check "Zoom To Mouse Position."  This lets you zoom in and out of the thing you are pointing at.
- Input: Select with: pick left.

### Cleaning out the Startup Configuration
Blender has a "Startup File". It is loaded everytime you slect "New File". Since X-Plane has its own camera, and lighting systems you may find it to be a time saver to remove them from the default.

1. For each item in the scene, right-click it in the outliner and pick "delete".
2. Pick File -> Save Startup File (or press Ctrl + U)

A tiny popup menu will appear under your mouse that says:
``
(?) Ok?
--------------------------
Save Startup File CTRL + U
``

- If you click "Save Startup File" the operation is confirmed and the save happens.
- If you move the mouse away, the operation is canceled.

This kind of "menu-based confirm" is heavily used in Blender.  It can be tricky to get used to at first, but can actually be very fast and natural.

### Customizing the Screen
Blender has a huge number of screens and lots of options to customize how the screen is organized.

Blender's default layout is good for general modeling, but I'm not a fan of the default UV editing view.  Here'es how to customize the view for texturing:
1. Start Blender
2. If you are not already in the "default" screen layout, pick that
3. Click the + sign next to the screen layout menu.  A new item Default.001 appears
4. Rename it to "texturing"
5. Put the mouse over the divide between the 3-d window and the main menu bar.  A horizontal pair of arrows will appear
6. Right click and pick "split area" - a vertical line appears. 
7. Move the mouse to put the line about at the midpoint of the main window and click
8. There are now two main editing areas
9. In the lower left corner of the right side window there is an icon with a cube and up-and-down arrows.  Pick it and select "UV/image editor
10. Put the main screen layout back to default
11. Pick File->save user startup file to save this change for future documents
