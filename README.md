# paper_met_o3_adj


This repository contains inputs and outputs used in the manuscript:

Title: Temperature and Stagnation Effects on Ozone Sensitivity to NOx and VOC: An Adjoint Modeling Study in Central California. 

Author: Yuhan Wang, Lucas Bastien, Yuan Wang, Ling Jin, and Robert Harley.


## Acronym
EP 224 = Baseline
EP 209 = High-T
EP 258 = Stagnation
met = meteorology inputs
emis = emission inputs
anth = anthropogenic emissions
bio = biogenic emissions
adj = adjoint model outputs
SARMAP = study domain name


## Note
The complete i/o dataset for all model runs are at ~TB level, and original data files are in netcdf format. To reduce data size, key files/variables are extracted and postprocessed into RData format here. For questions or access to original data, please contact yhanw@stanford.edu (Yuhan Wang). 


## Folder and file description

(1) "met" folder contains meteorological inputs used for CMAQ and adjoint simulations. 

Original data are in netcdf format. Four key variables above are extracted into RData arrays of 96 (x) * 117 (y) * 168 (hours) *  3 (episode) dimension:
PBL: Planetary boundary layer height (m)
temperature: surface temperature (K)
uwind.surface: surface wind u component (m/s)
vwind.surface: surface wind v component (m/s)

Example R code:
load("PBL.arr.RData")
print(arr[40,50,168,'224'])  # to find PBL at grid (40,50), last timestep (168) under baseline (ep 224) meteorology


(2) "grid" folder includes grid definition for crosswalk between x/y index and lat/lon. 

These are original CMAQ input files. Horizontal grid definitions are consistent across all three episodes.

(3) "emis" folder includes emission inputs.

The study includes 3 anthropogenic emission scenarios (2000, 2012, 2022) and 3 meteorological scenarios (ep 209, 224, 258). Biogenic emissions are driven by meteorology, so each meteorological scenario is associated with a unique biogenic emission inventory. Therefore, this folder includes 6 separate emission files (unit = mol/s):

bio.ep{$episode}.layer1: 4km-gridded biogenic emission at surface level, dimension = x*y*timestep*species
anth.yr{$year}.layer1:   4km-gridded anthropogenic emission at surface level, dimension = x*y*timestep*species

(4) "adj" folder includes original CMAQ adjoint model outputs.

There are 9 output files in total, each corresponding to a unique emission year (2000, 2012, 2022) and meteorology (ep 209, 224, 258) combination.
SARMAP_{$epsiode}_{$year}_CARB_EM_SUM.ADJPOST.nc

Each variable represents sensitivity of our "receptor" (i.e., San Joaquin Valley ozone metric) to unit emission change at each different grid cell. 



