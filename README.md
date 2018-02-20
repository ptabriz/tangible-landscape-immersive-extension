# Real-time 3D modeling and immersion with Tangibles
<img align="center" src="/documentation/img/Photo_collage.jpg" width=500>

## Abstract
We have paired GRASS GIS with Blender, a state-of-the-art 3D modeling
and rendering program, to allow real-time 3D rendering and immersion with Tangible Landscape. Tangible Landscape is a tangible interface for geographic information systems (GIS). It interactively couples physical and digital models of a landscape so that users can intuitively explore, model, and analyze geospatial data in a collaborative environment. Conceptually Tangible Landscape lets users hold a GIS in their hands so that they can feel the shape of the topography, naturally sculpt new landforms, and interact with simulations like water flow. As users manipulate a tangible model with topography and objects, geospatial analyses and simulations are projected onto the tangible model and perspective views are realistically rendered on monitors and head-mounted displays (HMDs) in near real-time. Users can visualize in near real-time the changes they are making with either bird’seye views or perspective views from human vantage points. While geospatial data is typically visualized as maps, axonometric views, or bird’s-eye views, human-scale perspective views help us to understand how people would experience and perceive spaces within the landscape.


#### How it works ####
Blender and GRASS GIS are loosely coupled through file-based communication established via a local wireless or Ethernet connection. GRASS GIS exports the spatial data as a standard raster, a vector, or a text file containing coordinates into a specified directory typically called Watch (Figure setup). The Tangible Landscape Blender plugin (modeling3D.py)—implemented and executed inside Blender— constantly monitors the directory for incoming information. Examples of spatial data include a terrain surface (raster), water bodies (3D polygons or rasters), forest patches
(3D polygons), a camera location (3D polyline, text file), and routes (3D polylines).
Upon receiving this information, the file is imported using the BlenderGIS add-on.
Then the relevant modeling and shading procedures for updating an existing 3D
object or creating a new 3D object are applied. The adaptation procedure applied
depends upon the type of spatial data and is handled by a module called adapt. All
3D elements in the scene (i.e. objects, lights, materials, and cameras) reside in a
Blender file (modeling3D.blend).
<img src="documentation/img/coupling_schema.jpg" width=500>

## Dependencies
-   [Blender 2.79](https://www.blender.org/download/)
-   [BlenderGIS addon](https://github.com/domlysz/BlenderGIS)
-   [Blender virtual_reality_viewport addon](https://github.com/dfelinto/virtual_reality_viewport)

## Installation
#### 1. Installing and setting up Tangible landscape addon in Blender
  * Open Blender ``user preferences`` (Alt + Ctrl + U) > Go to ``add-ons`` tab > ``Install from file`` (bottom center of the panel) > locate TL_addon.zip > press enter
  * Select on the addon to activate it.
  * In the ``Preferences`` tab > ``Coupling folder`` > browse and locate TL_coupling folder (e.g, D:/TL_coupling)
  * In the ``Coordinate reference system`` field type-in the 4 digit EPSG code related to your GIS dataset. The provided examples use 3358.
  * Click on ``Save User Settings`` on the bottom left corner of user preferences
#### 2. Installing and setting up Blender virtual_reality_viewport addon
  * Install and activate BlenderGIS addon (for detailed instruction see [BlenderGIS wiki](https://github.com/domlysz/BlenderGIS/wiki/Install-and-usage))
  * Go to ``Preferences`` > ``BlenderGIS preferences`` > ``Spatial reference system`` > add your EPSG 4 digit code and a description  (e.g., 3358 , NAD 1983)
  * From the ``Import/Export panel`` deactivate ``Adjust 3D view`` and ``Force textured solid shading``.
  * Click on ``Save User Settings`` on the bottom left corner of user preferences
#### 3. Installing and setting up Blender virtual_reality_viewport addon
  * Install and activate VR addon (for detailed instruction see [addon installation guide](https://github.com/dfelinto/virtual_reality_viewport)
  * Click on ``Save User Settings`` on the bottom left corner of user preferences
#### 4. Optimizing the blender scene
In this step we adjust system settings to optimize the viewport rendering performance.
  * In the ``Blender User Preferences`` > ``System`` :
    * In ``General`` section > adjust ``DPI``to increase/decrease icon size based on your preferences and monitor resolution.
    * In ``OpenGL``section > deactivate ``Mipmaps`` , ``GPU Mipmap Generation``, and ``16Bit Float Textures``
    * Set ``Selection`` to Automatic
    * Set ``Anistropic filtering`` to Off
    * Set ``Window Draw Method`` to Automatic and No MultiSample
    * Deactivate ``Text Anti-aliasing``
    * In ``Texture`` section set ``Texture limit size`` to Off
    * Set ``Images Draw Method`` to GLSL
  * Click on ``Save User Settings`` on the bottom left corner of user preferences
## Real-time modeling example
For testing the real-time modeling you can manually copy sample geospatial data from test folder to the watch folder.  
* Inside the test folder you can find the following sample data are provided:
  * Terrain raster (terrain.tif)
  * Water raster (water.tif)
  * Multiple vantage points (vantage.shp)
  * 4 tree patches (patch_class1.png, patch_class2.png, patch_class3.png, patch_class2.png)
  * Trail (trail.shp)
* Download the modeling3D.Blend from here.
* Open modeling3D.Blend
* Locate Tangible landscape panel from ``Toolshelf`` and click on ``Turn on Watch mode``
* Copy the test files in one by one starting with the terrain to the ``Watch folder``.
* Cancel Watch mode at anytime using Right-click or Scape while mouse cursor is in 3D views
* Toggle Maximize view using ``Ctrl + Up`` or full screen using ``Alt + F10``
## Addon features
* ``Watchmode`` button activates the modal timer
function and waits for the Geospatial data to be copied to the Watch
folder.
* ``Camera options`` allows user to toggle between the following
four camera types: human view camera linked to the tangible view marker, preset bird views, preset human views, and a bird view camera dedicated
to an animated orbiting bird view camera. The preset bird and human cameras
are linked to the 3D viewport allowing users to navigate the 3D scene (with the
mouse), adjust and revisit their preferred views.
* ``The Rendering and realism`` panel includes buttons for selecting between Cycle and Blender Render engines, and between low-poly and realistic representations. Note : ``Low poly`` rendering is only supported in ``Cycle mode``



### Using your own data
![Immersive extension GUI](https://github.com/tangible-landscape/tangible-landscape-immersive-extension/blob/master/blob/blender_gui_1.PNG)
