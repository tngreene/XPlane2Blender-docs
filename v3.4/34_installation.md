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
1. Download XPlane2Blender. The safest choice (see "[What Version Do I Choose?](link)") is the latest **non pre-release** [version](https://github.com/der-On/XPlane2Blender/releases). Put it in a convenient place
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

If it is not located in one of these places, you'll have to find it yourself. You can change the location of the scripts folder in User Preferences, however this could affect other addons. Proceed with caution.

#### Official Blender Documentation
- [Configuring Directories](https://docs.blender.org/manual/en/dev/getting_started/installing/configuration/directories.html)

## Customizing Blender
### Preferences to change
From File->Preferences, a few settings I like to customize to make Blender easier to use:
- Interface Tab: check "Zoom To Mouse Position."  This lets you zoom in and out of the thing you are pointing at.
- Input: Select with: pick left.

### Cleaning out the Startup Configuration
Blender has a "Startup File". It is loaded everytime you select "New File". Since X-Plane has its own camera, and lighting systems you may find it to be a time saver to remove them from the default.

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
An important part of an efficient workflow is customing your screen layout. You can read more about it on Blender's manual
- [Screens Overview](https://docs.blender.org/manual/en/dev/interface/window_system/screens.html) 
- [Area Splitting and Resizing](https://docs.blender.org/manual/en/dev/interface/window_system/areas.html)
