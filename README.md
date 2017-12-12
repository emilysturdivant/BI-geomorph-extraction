# BI-geomorph-extraction
Author: Emily Sturdivant; esturdivant@usgs.gov

This repository contains a python package (CoastalVarExtractor) to calculate coastal geomorphology variables along shore-normal transects. It is used to produce inputs for modeling geomorphology using a Bayesian Network and is a companion to a Methods Open-File Report (Zeigler and others, 2018) and various ScienceBase data releases that have been or will be published (e.g. Gutierrez and others, 2018). The repo also includes a 'notebooks' folder, which document the implementation instances of the code that produced the published datasets. 

The Methods OFR is titled "Evaluating barrier island characteristics and piping plover (Charadrius melodus) habitat availability along the U.S. Atlantic coast - geospatial approaches and methodology."

## Requirements
ArcGIS Pro, which includes an installation of Anaconda and Python 3.

## Installation

```python
\ArcGIS\Pro\bin\Python\Scripts\proenv
pip install 
```

## How to implement:

1. Acquire all input feature classes - refer to input variables in addition to the list below. 
    - transect lines
    - DH points
    - DL points
    - shoreline points
    - DEM
    
2. Review values (mostly file paths) in setvars.py and update if needed.

3. Interactively run prepper.ipynb from the ArcGIS Pro to make some of the input files. There are steps in the process that must be completed manually. Notes in the script describe the procedure for creating them. 
    - inlet lines <- DEM + **manual**
    - armoring lines <- ortho + **manual**
    - boundary polygon <- DEM + shoreline points + inlet lines (+ manual)
    - oceanside MHW shore between inlets <- boundary polygon + inlets 
    - supplemented and sorted transects <- script + **manual**; Sorting is only semi-automated and tricky. See explanations below/in prepper.ipynb.
    - 'tidied' extended transects <- script + **manual**

4. QA/QC/cross-check everything thoroughly: projections, agreement, etc. Preferred projection is NAD83, Meters - Albers or UTM Zone 18N or 19N depending on region of Atlantic coast.

5. Run extractor.ipynb.

## Notes about using ArcPy

Jupyter notebook files must be run within the ArcGIS Pro conda environment. To do so, type the following in your command prompt (assuming it has the default set-up and substituting path\to\dir with the location of the repository):

```
cd path\to\dir\BI-geomorph-extraction
\ArcGIS\Pro\bin\Python\Scripts\proenv
jupyter notebook
```
