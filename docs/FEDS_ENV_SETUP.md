# FEDS Environment Setup on Derecho

Environment name: feds_py39  
Location: /glade/u/home/zke3/micromamba/envs/feds_py39  
Created: Feb 2026  

## Step 1 — Create environment
module load conda
conda install -n base -c conda-forge mamba
mamba create -n feds_py39 -c conda-forge \
  python=3.9 \
  numpy=1.21 \
  pandas=1.3 \
  geopandas=0.9 \
  xarray=0.18 \
  scipy=1.7 \
  shapely=1.8 \
  pyproj=3.2 \
  gdal=3.4 \
  fiona \
  rasterio \
  rtree

## Step 2 — Activate

mamba info --envs
conda activate /glade/u/home/zke3/micromamba/envs/feds_py39


## Step 3 — Register Jupyter kernel

python -m ipykernel install --user \
  --name feds_py39 \
  --display-name "Python (FEDS py39)"

## Verify imports

python - << 'EOF'
import numpy, pandas, geopandas, xarray, scipy, shapely, pyproj
from osgeo import gdal
print("Environment OK")
EOF


