# Creating Map Overviews

A map overview requires two files: a bitmap (.bmp) image and a description file (.txt).  Both files are placed in `<dod>/overviews` and should be added to the map's `.res` file.

## Acquiring Image from In-Game

- Set `-dev` for the launch options in Steam
- Launch the game
- Configure Video Settings
  - Set `Display Mode` to `Normal` (if on `Widescreen`)
  - Set `Resolution` to `1024x768`
  - (Recommended) Check `Run in a window`
  - Apply Settings (this will restart the game)
- Start the map with `map <mapname>` in console
- Set the following cvars:
  - `sv_cheats 1`
  - `_cl_minimap 0`
  - `developer 0`
  - `net_graph 0`
  - `dev_overview 2`
  - `hud_draw 0`
- Ajust the view using the commands in the table below
- Take a `snapshot` (default `F5`)
- Set `dev_overview 1` and copy the parameters shown in console
  - Example console output:
    ```
    Overview: Zoom 1.24, Map Origin (-717.67, 196.00, -96.00), Z Min 449.00, Z Max -641.00, Rotated 1
    ```
- Clean up:
  - Set `Display Mode` back to `Widescreen`
  - Set `Resolution` back to desired resolution
  - Uncheck `Run in a window`
  - Apply changes
  - Exit the game
  - Remove `-dev` from the launch options


### View Adjustment Commands

| Command    | Action                                                 | Corresponding Action in a Normal Game       |
|------------|--------------------------------------------------------|---------------------------------------------|
| +forward   | shifts the screen to the left [^1]                     | walk forward                                |
| +backward  | shifts the screen to the right [^1]                    | walk backward                               |
| +moveright | shifts the screen up [^1]                              | strafe right                                |
| +moveleft  | shifts the screen down [^1]                            | strafe left                                 |
| +jump      | increases Z max value (removes floors from the bottom) | jump                                        |
| +duck      | decrease Z max value (adds floors from the bottom)     | duck                                        |
| +moveup    | increase Z min value (adds floors from the top)        | move upwards on a ladder or in water        |
| +movedown  | decrease Z min value (removes floors from the top)     | move downward on a ladder or in water       |
| +attack1   | increase zoom factor                                   | primary firing button                       |
| +attack2   | decrease zoom factor                                   | alternate firing and zoom button            |

[^1]: If the map is rotated, the forward/backward and moveright/moveleft will be swapped

## Editing Overview Image

The bitmap (.bmp) must be edited to be used for a map overview.  The file must be saved as `<mapname>.bmp`.

### BMP Image File Format

- Image Mode:  `Indexed`
- Color Count:  `256`
- Transparency Color:  `0x00ff00`
- Compatibility:  Do not write color space information

If transparency is needed/used, one of the 256 colors should be assigned as `0x00ff00`.


## Overview Description File

Create `<mapname>.txt` based on the following template using the parameters obtained with `dev_overview 1` where `HEIGHT` is the `Z Max` value.

```
// overview description file for <mapname>.bsp

global 
{
	ZOOM		1.11
	ORIGIN		-150.75	-1021.05	-576.00
	ROTATED		1
}

layer 
{
	IMAGE	"overviews/<mapname>.bmp"
	HEIGHT	-2305.00
}
```

