# Changelog 

## 0.1.0 2026-05-27

### Added
- Initial experimental release.
- Select one or more DEM raster layers.
- Build a VRT mosaic for multiple selected rasters.
- Reproject DEMs to a target CRS.
- Optionally clip output using a saved polygon AOI mask layer.
- Fill NoData pixels before scaling, using either a user-specified elevation value or the minimum valid elevation.
- Rescale output values to 0–65535.
- Export Blender-ready UInt16 GeoTIFF files.
- Basic GDAL argument fields for merge, warp, clip, and translate steps.