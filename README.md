# QGIS Plugin Adjust Style
[QGIS Plugin](https://plugins.qgis.org/plugins/qgis_adjust_style/) to adjust the symbology of a map with a few clicks instead of altering every single symbol (and symbol layer) for many layers, categories or for a number of label rules. It offers a quick way to change the style of all layers (or selected layers) consistently, to check out how different colors / stroke widths / fonts work for a project, and to save and load styles of all layers at once – or even to apply styles to another project. 

With one mouse click, it allows to (in all seleced layers): 
- adjust color using the HSV color model: rotate hue (think of a color wheel), change saturation and value: 
    - all symbols (with any number of symbol layers) including color ramps used in graduated / categorized / heatmap renderers
    - colors used in paint effects (glow, shadow)
    - color ramps in raster pseudocolor
    - raster layers using the colorize option
    - labels (text color, background color, text buffer color)
    - background color of the map canvas of the project
    - colors in annotations
- change stroke width (i.e. line thickness) of all lines and borders of markers and polygons 
- change font size of all labels and annotations 
- replace a font family used in labels / annotations with another font family
- save / load the styles (QML files) of layers into/from a given folder 
- replace font family or change font size everywhere in a print layout
- change colors or stroke width in a print layout


![QGIS plugin adjust style](help/screenshot.png)


## Install

The plugin is in the [QGIS Plugins Repository](https://plugins.qgis.org/plugins/qgis_adjust_style/) and can be installed directly from QGIS (menu: Plugins > Manage and Install Plugins). Eventually, the checkbox to also show experimental plugins must be checked in the settings of the plugin manager.

Alternatively, copy (or git clone) the folder with the code into your QGIS plugin folder and enable the plugin in QGIS (menu: Plugins > Manage and Install Plugins).

## Usage
Start the plugin from the plugin menu or the plugin toolbar; a dockwidget opens on the right side of the main window.

Another dockwidget is available in the layout composer window (since version 1.9).

The "change by" slider / spin box sets the strength of the change in the range of 5 to 90. Stroke width or font size will be increased / decreased by a corresponding percentage. When changing HSV color saturation or value, the value is added / substracted as absolute value (in the range 0 to 255).

### Select Layers or Print Layout Components
First, select the layers you want to work on. Possible choices:
- Active Layer
- Selected Layers
- Visible Layers
- All Layers 
Optionally check to include:
- Main Annotation Layer (ignored with QGIS < 3.22)
- Canvas background color

The dockwidget for print layout has the following choices:
- Labels (text boxes)
- Legend
- Scalebar
- North arrow and parameterized SVG
- Shapes (rectangles, circles, triangles)
- Marker
- Lines, Polygons, Arrows
- Tables
- Page Background 

### Change Color
Adjusting colors works in the HSV color model. That means you can rotate the hue of the HSV colors as you would rotate a color wheel: set the degree of the rotation and hit "OK". The color grid above the slider works as a preview.

To adjust saturation and value (= brightness), click on the respective plus and minus buttons. Be careful: You can't use the plus and minus button to undo the changes already made, because: 
- saturation and HSV value stay in the interval ranging from 0 to 255 and any color arriving at these borders can't be moved back in an consistent way. 
- fully desaturating any color results in the complete loss of the hue, as achromatic colors (i.e. saturation of 0; white, black, grey) do not have a hue.

It is good practice to save the layer styles before using these buttons!

### Stroke Width
Change the stroke width of lines and of the borders of polygons and point markers with clicks on the plus and minus buttons. Also works for raster layers with contour renderer.

Note: Hairlines remain hairlines.

### Labels
Note: Changing the color of layers also changes the color of labels (text, buffer and background color).

#### Font Size
Use the plus / minus buttons to change the font size of labels in increments of 5 %.

#### Replace Font
Choose the font family to be replaced and select a new font family.

### Annotations
With the checkbox "Main Annotation Layer" checked, all marker symbols and text elements of the main annotation layer of the project are changed. If you are using additional annotation layers, they are counted as layers with the active / selected / visible / all layers comboboxes. 

### Save and Load Styles
These buttons provide a quick way to save the styles of all (or all selected) layers. You only need to select a folder. The filename of the QML files corresponds to the layer name (with bad characters replaced by underscore). If there are several layers of the same name, you will get several files with an index value appended. 

With "Canvas Background" checked, the background color of the project is loaded/saved as well (a simple text file with color in hex notation).

#### Apply a map style to another project
It even works to save the styles of one project and load them in another one if the layer names of the projects match. If not, you can still save the styles of all layers and apply them to individual layers by loading the respective QML file from the QGIS layer properties dialog.

## Bug Tracker
[https://github.com/florianneukirchen/qgis_adjust_style/issues](https://github.com/florianneukirchen/qgis_adjust_style/issues)

## Change Log

### 2.0 (2024-09)
- First stable release with the new dock in the layout designer window
- Implement color change on Mesh layers
- Implement color change of the new single color renderer
- Set initial "change by" to 10

### 1.9 (2024-08, Development version)
- Code refactoring
- Allow to set the strength of the change (from 5 to 90, used as absolute value for HSV color parts and as percentage for sizes)
- Implement another dock widget for the layout designer window to adjust the style of layout items 
- Set minimum QGIS version to 3.30 (changes to legend in print layout don't work with older versions)
### 1.3 (2024-02)
- Implement adjusting Filled Line (new in QGIS 3.36)
- Set QGIS minimum version to 3.22, as not everything was working in QGIS 3.16
- Catch exception with replace font dialog if selection does not contain any fonts
- Update German translation
### 1.2 (2023-06)
- Change color / font size of annotations a.k.a. annotation layers, also fixes a crash (issue #4)
- Change stroke width of lineburst lines (issue #3)
- Now also works on interpolated lines
- Fix issue #2: Color ramps used in glow paint effect are not modified
- Catch an exception (issue #8)
### 1.1 (2023-06)
- Fix typo in plugin name in metadata (issue #1)
### 1.0 (2023-05)
- Change stroke width and font size by 5 % instead of a small absolute value, to make it work in map units
- Changing stroke works for most renderer and symbol types now, including subsymbols (such as marker line)
- Shapeburst and lineburst: correctly change color ramp and color2
- Raster: Change color ramp of single band pseudo color renderer
- Raster layers with colorize in the render pipeline: change color
- Change colors in vector layer effects (glow, shadow)
- Mark strings for translation
- Add German translation
- Flag project as modified ("dirty") after changing / loading the style
- Do not crash on QgsNullSymbolRenderer
- Change color ramp of heatmap renderer
- Change color and stroke on raster contour renderer
- Option to change background color of map canvas as well
- Fix message on loading styles with style files for only some layers
- Add tooltips

### 0.2 (2023-05)
- Do not crash on a QgsGroupLayer (this is a new QGIS feature)
- Fix crash of changing stroke width with renderers other than line and simple fill

### 0.1 (2023-05)
- Initial release


