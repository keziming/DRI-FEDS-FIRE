# NLCD 2016 Land Cover Setup (California)

Purpose: Prepare NLCD 2016 land cover raster for FEDS processing.

Last updated: Feb 2026  
Machine: Derecho  

---

## Step 1 — Go to working directory

cd /glade/u/home/zke3/scratch/IMP_fire_2026/ExtData

---

## Step 2 — Download NLCD 2016 (PASDA mirror)

wget -c https://www.pasda.psu.edu/download/usgs/NLCD2016/NLCD_2016_Land_Cover_L48_20190424.zip

---

## Step 3 — Unzip

unzip NLCD_2016_Land_Cover_L48_20190424.zip

Expected file:
nlcd_2016_land_cover_l48_20190424.img

---

## Step 4 — Convert to GeoTIFF

module load gdal

gdal_translate nlcd_2016_land_cover_l48_20190424.img nlcd_full.tif

---

## Step 5 — Clip roughly to California bbox (fast)
## Use screen command, these calculations take time (step 5~7)
gdalwarp \
  -te -125 32 -113 42 \
  -te_srs EPSG:4326 \
  -r near \
  -dstnodata 0 \
  nlcd_full.tif nlcd_bbox.tif

---

## Step 6 — Clip precisely to California boundary

gdalwarp \
  -cutline ./Calshape/California.shp \
  -crop_to_cutline \
  -dstnodata 0 \
  -r near \
  nlcd_bbox.tif nlcd_CA.tif

---

## Step 7 — Convert to FEDS expected format

FEDS expects a lat/lon GeoTIFF named:

/glade/u/home/zke3/scratch/IMP_fire_2026/ExtData/nlcd_510m.tif

gdalwarp \
  -t_srs EPSG:4326 \
  -tr 0.005 0.005 \
  -r near \
  nlcd_CA.tif nlcd_510m.tif

---

## Quick Sanity Check

gdalinfo nlcd_510m.tif | grep EPSG
gdalinfo nlcd_510m.tif | grep "Size is"

Expected:
- EPSG:4326
- Pixel size ~0.005 degree

# Use screen command, these calculations take time (step 5~7)
