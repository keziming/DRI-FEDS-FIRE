# VIIRS VNP14IMGML Download (2012–2020)

Purpose: Download VIIRS active fire monthly ASCII data
(VNP14IMGML Collection 1) for FEDS processing.

Last updated: Feb 2026  
Machine: Derecho  

---

## Data Source

UMD server (documented in user guide)

Server:
fuoco.geog.umd.edu

Login:
fire

Password:
burnt

---

## Step 1 — Connect via SFTP

On Derecho:
# go to where you want to save the VIIRS data
cd /glade/u/home/zke3/scratch/IMP_fire_2026/ExtData/VNP14IMGML04

sftp fire@fuoco.geog.umd.edu

Enter password when prompted.

---

## Step 2 — Navigate to Collection-1 directory

Inside SFTP:

ls
cd data
ls
cd VIIRS
ls

You are looking for:

C1/VNP14IMGML/

Specifically Collection 1.04 (C1.04),
which matches the naming used in FEDS.

---

## Step 3 — Download All Years (2012–2020)

Inside the correct directory:

cd PATH_TO_C1_04_DIR

mget VNP14IMGML.2012*.C1.04.txt
mget VNP14IMGML.2013*.C1.04.txt
...
mget VNP14IMGML.2020*.C1.04.txt

Or use:

mget VNP14IMGML.201*.C1.04.txt
mget VNP14IMGML.2020*.C1.04.txt

When finished:

bye

---

## Expected File Format

Example filename:

VNP14IMGML.201201.C1.05.txt.gz

Files contain monthly ASCII fire detections.

Columns include:
- YYYYMMDD
- HHMM
- Satellite
- Latitude
- Longitude
- FRP
- Radiative power
- Confidence
- Land cover
- etc.

---

## Notes

- Product: VIIRS Active Fire Monthly ASCII
- Version: Collection 1 (C1.04/C1.05)
- Temporal coverage used: 2012–2020
- Used for: Fire detection input to FEDS

