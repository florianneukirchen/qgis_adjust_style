# QGIS Plugin Adjust Style
[QGIS Plugin](https://plugins.qgis.org/plugins/qgis_adjust_style/) to adjust the style of a map with a few clicks instead of altering every single symbol (and symbol layer) for many layers, categories or for a number of label rules. It offers a quick way to adjust the style of all layers (or selected layers) consistently, to check out how different colors / stroke widths / fonts work for a project, and to save and load styles of all layers – or even to apply styles to another project. 

With one mouse click, it allows to (in all seleced layers): 
- adjust color of all symbols (including color ramps and any number of symbol layers) and labels using the HSV color model (rotate hue, change saturation and value)
- change line thickness (i.e. stroke width of all symbols / symbol borders)
- change font size of all labels
- replace a font family used in labels with another font family
- save / load the styles of layers into/from a given folder.

![QGIS plugin adjust style](help/screenshot.png)


## Install
The plugin is in the [QGIS Plugins Repository](https://plugins.qgis.org/plugins/qgis_adjust_style/) and can be installed directly from QGIS (menu: Plugins > Manage and Install Plugins). In the settings of the plugin manager, the checkbox to also show experimental plugins must be checked.

Alternatively, copy (or git clone) the folder with the code into your QGIS plugin folder and enable the plugin in QGIS (menu: Plugins > Manage and Install Plugins).

## Usage
Start the plugin from the Plugin menu or the plugin toolbar, a dockwidget opens on the right side of the main window.

### Select Layers
First, select the layers you want to work on. Possible choices:
- Active Layer
- Selected Layers
- Visible Layers
- All Layers

### Change Color
Adjusting colors works in the HSV color model. That means you can rotate the hue of the HSV colors as you would rotate a color wheel: set the degree of the rotation and hit "OK". The color grid above the slider works as a preview.

To adjust saturation and value (= brightness), click on the respective plus and minus buttons to adjust the respective value ± 5. Be careful: You can't use the plus and minus button to undo the changes already made since saturation and HSV value stay in the interval ranging from 0 to 255 and any color arriving at these borders can't be moved back in an consistent way. 

It is good practice to save the layer styles before using these buttons!

### Stroke Width
Change the stroke width of lines and the borders of polygon symbols and point symbols with clicks on the plus and minus buttons. 

Stroke width is increased/decreased by 5 %; the change is subtle and may only be visible after several clicks. Hairlines remain hairlines.

### Labels
Note: Changing the color of layers also changes the color of labels (text, buffer and background).

#### Font Size
Use the plus / minus buttons to change the font size of labels in increments of 5 %.

#### Replace Font
Choose the font family to be replaced and select a new font family.

#### Save and Load Styles
These buttons provide a quick way to save the styles of all (or all selected) layers. You only need to select a folder. The filename of the QML files corresponds to the layer name (with bad characters replaced by underscore). If there are several layers of the same name, you will get several files with an index value appended. 

Should even work to save the styles of one project and load them in another one if the layer names match. 

## Change Log
### 1.0 
- Change stroke width and font size by 5 % instead of a small absolute value, to make it work in map units
- Changing stroke works for most renderer and symbol types now, including subsymbols (such as marker line)
- Shapeburst and lineburst: correctly change color ramp and color2
- Raster: Change color ramp of single band pseudo color renderer
- Raster layers with colorize in the render pipeline: change color
- Change colors in vector layer effects (glow, shadow)
- Mark strings for translation
- Add german translation
- Flag project as modified ("dirty") after changing / loading the style
- Do not crash on QgsNullSymbolRenderer
- Change color ramp of heatmap renderer
- Change color and stroke on raster contour renderer
- Fix message on loading styles with style files for only some layers

### 0.2 (2023-05)
- Do not crash on a QgsGroupLayer (this is a new QGIS feature)
- Fix crash of changing stroke width with renderers other than line and simple fill

### 0.1 (2023-05)
- Initial release

## Known Bugs / Limitations
- Annotations (annotation layers) are not changed
- Color ramps: color brewer ramps are not modified 
- Changing stroke width does not work for symbol layers based on QgsAbstractBrushedLineSymbolLayer such as lineburst

## Bug Tracker
[https://github.com/florianneukirchen/qgis_adjust_style/issues](https://github.com/florianneukirchen/qgis_adjust_style/issues)


