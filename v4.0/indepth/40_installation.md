# Installation

## Download and Install Blender
Go to [the Blender home page](https://www.blender.org/download/) and download Blender. For specific OS questions, [read the Blender Manual](https://docs.blender.org/manual/en/latest/getting_started/installing/index.html). If you need to use Blender 2.79 or older you'll need to pick your XPlane2Blender version accordingly.

### Automatic Installation
It is __an extremely good idea__ to let Blender install and remove addons for you. Blender is extremely picky - it is surprisingly easy to put the addon in the wrong place. See troubleshooting at the bottom if something goes wrong.

1. Download the latest [XPlane2Blender release candidate](https://github.com/X-Plane/XPlane2Blender/releases/latest). You want the .zip file with a name like ``io_xplane2blender_4_0_0-rc_1-89_20200910152046.zip``
(look under **Assets** at the bottom of the release notes). **Do not download "Source code (zip)".**
2. Launch Blender and open the "Preferences" Window (`Edit->Preferences`).
3. Select the "Add-ons" tab
4. Click `"Install from File..."`, ensure `"Overwrite"` is checked
5. Use the Blender file picker to select the .zip file you downloaded in step 1
6. Ensure the addon is enabled (the check in the checkbox next to the words "Import-Export: Export: X-Plane (.obj)")
![](./content/addon_panel_addon_enabled.png)
7. **Restart Blender**, even if you see the correct UI!
8. Look in the Scene Properties to see that your version matches the file you downloaded

See the Blender manual's [Addons section](https://docs.blender.org/manual/en/latest/editors/preferences/addons.html) for more details.

[Alpha and beta releases](https://github.com/X-Plane/XPlane2Blender/releases) have cutting edge features but are more likely to have bugs in them. Use with caution and please submit bug reports! Older and other versions of XPlane2Blender (like the converter) may require a different version of Blender. Whatever you pick, always make backups of your work.

> If Auto-save settings is unchecked, you'll have to click "Save User Settings" before exiting the Preferences Window.

### Troubleshooting
The largest sources of problems, in order, are
1. Attempting to install the addon by hand. There are so many surprising ways to get it wrong
2. **Not downloading** the .zip file with a name like `io_xplane2blender_4_0_0-rc_1-89_20200910152046.zip`. The .zip file called "Source Code" will not automatically install
3. Not restarting Blender, especially after updating to a new version of the addon

If restarting Blender doesn't work, delete anything related to `XPlane2Blender` or `io_xplane2blender` from your `scripts` and `addons` folder.

The folders are typically found (replace `2.80` with your Blender version) in following places
- macOS: ``/Users/$USER/Library/Application Support/Blender/2.80/scripts/addons``
- Windows: ``%USERPROFILE%\AppData\Roaming\Blender Foundation\Blender\2.80\scripts\addons``
- Linux: ``$HOME/.config/blender/2.80/scripts/addons``

(The `addons` folder is created for you by Automatic Installation. You don't need to make it manually if you follow these instructions.)

After that retry following the **Automatic Installation** instructions exactly as written. If it still doesn't work, file a bug.
