# California Boundary Shapefile Setup (FEDS)

Purpose: Prepare a clean California boundary shapefile in EPSG:4326
for filtering FEDS fire pixels.

---

## Step 1 — Go to working directory

cd /glade/u/home/zke3/scratch/IMP_fire_2026/ExtData/Calshape

---

## Step 2 — Download Census 1:500k state boundary

wget https://www2.census.gov/geo/tiger/GENZ2021/shp/cb_2021_us_state_500k.zip

unzip cb_2021_us_state_500k.zip

---

## Step 3 — Extract California only

module load gdal

ogr2ogr -overwrite -f "ESRI Shapefile" California.shp \
  cb_2021_us_state_500k.shp \
  -nln California \
  -where "NAME='California'"

---

## Step 4 — Check projection

ogrinfo -so California.shp California

Expected CRS: EPSG:4326 (WGS84)

---

## Step 5 — Reproject (if needed)

If not EPSG:4326:

ogr2ogr -t_srs EPSG:4326 California.shp cb_2021_us_state_500k.shp

---

## Notes

- Source: US Census Cartographic Boundary
- Resolution: 1:500k
- Used for: FEDS spatial filtering and clipping
- CRS required: EPSG:4326 (lat/lon)

