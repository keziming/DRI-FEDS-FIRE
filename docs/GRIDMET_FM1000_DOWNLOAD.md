# GridMET fm1000 (1000-hr Fuel Moisture) Download

Purpose: Download and verify GridMET 1000-hour dead fuel moisture
for use in FEDS analysis.

Last updated: Feb 2026  
Machine: Derecho  

---

## Step 1 — Go to working directory

cd /glade/u/home/zke3/scratch/IMP_fire_2026/ExtData/GridMET

---

## Step 2 — Download all years (2012–2020)

for y in {2012..2020}; do
  echo "Downloading $y"
  wget -c https://www.northwestknowledge.net/metdata/data/fm1000_${y}.nc
done

---

## Step 3 — Verify file contents

Check that the required variable exists:

ncdump -h fm1000_2012.nc | grep dead_fuel_moisture_1000hr

Expected variable:

dead_fuel_moisture_1000hr

---

## Notes

- Dataset: GridMET
- Variable: dead_fuel_moisture_1000hr
- Units: Percent
- CRS: WGS84 (EPSG:4326)
- Dimensions: lon, lat, time
- Years downloaded: 2012–2020

