# QGIS2Blender

QGIS2Blender is a QGIS plugin for preparing DEMs for use in Blender heightmap workflows. It is inspired by [Daniel Huffman’s shaded relief process in Blender](https://somethingaboutmaps.wordpress.com/2017/11/16/creating-shaded-relief-in-blender/).

## What it does

QGIS2Blender lets you select one or more DEM raster layers and export them as Blender-ready heightmaps.

The plugin can:

- combine multiple DEMs using a virtual raster (VRT)
- reproject the data to a target CRS
- optionally clip the data to an area of interest using a polygon mask layer
- fill NoData pixels before scaling using either a user-specified elevation value or the minimum valid elevation
- rescale raster values to `0–65535`
- export the result as a 16-bit unsigned integer (`UInt16`) GeoTIFF

## Installation

### From the QGIS Plugin Repository:
QGIS2Blender has been accepted as part of the [QGIS official plugin repository](https://plugins.qgis.org/plugins/qgis_blender/). It can be installed in QGIS from `Plugins` > `Manage and Install Plugins`

### From ZIP

1. Download the latest release ZIP from the GitHub releases page.
2. Open QGIS.
3. Go to **Plugins → Manage and Install Plugins…**
4. Choose **Install from ZIP**.
5. Select the downloaded ZIP file.
6. Enable **QGIS2Blender** in the Plugin Manager.

## Basic workflow

1. Import the DEMs you want to process into your QGIS project.
2. Optional: create or import a polygon layer to use as an area-of-interest mask.
3. Open **QGIS2Blender**.
4. Select the DEM raster layer(s) you want to export.
5. Choose the CRS using the CRS selector.
6. Optional: select a polygon AOI mask layer. If no mask layer is selected, the plugin exports the full selected raster or raster mosaic extent.
7. Choose a NoData value. Default value is the minimum valid terrain height. The NoData fill value is included in the scaling range. Values far outside the DEM’s elevation range may reduce height contrast in the final heightmap.
8. Choose an output file location.
9. Click **Run**.
10. Import the resulting GeoTIFF into Blender following a workflow such as [Daniel Huffman’s tutorial](https://somethingaboutmaps.wordpress.com/2017/11/16/creating-shaded-relief-in-blender/).

## AOI mask notes

If you use a polygon AOI mask, the plugin clips the output to that polygon layer.

For best results, create the AOI polygon in the same CRS you plan to use as the target CRS. If the AOI layer uses a different CRS, the output may not align as expected.

Use a saved polygon layer, such as a shapefile. Temporary or scratch layers may not work reliably, especially on Windows.

## Output behavior

QGIS2Blender is designed for Blender heightmap export, not for preserving original elevation values.

Before scaling, NoData pixels are filled with a user-specified value in the DEM’s elevation units. If left blank, NoData is filled with the minimum valid elevation before scaling. The NoData fill value is included in the scaling range. Values far outside the DEM’s elevation range may reduce height contrast in the final heightmap.

The final output is rescaled to `0–65535` and exported as `UInt16`. This makes it suitable for Blender heightmap workflows, but the output should not be treated as a DEM with original elevation units.

## Known limitations

- - AOI clipping currently requires a polygon mask layer.
- If no AOI mask is selected, the full selected raster or VRT mosaic extent is exported.
- AOI masks should be saved as vector layers. Temporary layers may not work reliably. 
- Output values are rescaled for Blender and do not preserve original elevation values.
- Advanced smoothing and resampling controls are not yet included.

## License

Copyright (C) 2026 Ben Leamon

This program is free software; you can redistribute it and/or modify it under the terms of the GNU General Public License as published by the Free Software Foundation; either version 2 of the License, or (at your option) any later version.

This program is distributed in the hope that it will be useful, but WITHOUT ANY WARRANTY; without even the implied warranty of MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE. See the GNU General Public License for more details.

You should have received a copy of the GNU General Public License along with this program; if not, see <https://www.gnu.org/licenses/>.