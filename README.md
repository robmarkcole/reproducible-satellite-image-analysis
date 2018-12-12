# Reproducible-satellite-image-analysis
Whilst there are many well written articles on performing satellite image analysis, it is often a frustrating experience trying to reproduce them owing to lack of detail about the package environment or broken links to imagery. This repository seeks to demonstrate best practice for allowing reproducible analysis, by using Binder to host a perfect reproduction of the analysis environment, complete with dependencies and required imagery data.

## Conda
Use a conda environment to isolate required packages, and write an `environment.yaml` file to allow Binder to recreate the environment. Conda makes installing packages such as Rasterio straightforward, handling installation of their C++ dependencies for you (GDAL!). Using Conda environments with Jupyter notebooks is a bit of a hassle, but this won't be a problem on Binder. 

## Data
Github allows large files to be uploaded, although these should be kept to a minimum. If more than a couple of satellite images are required for analysis, it is best to put them in a public S3 bucket.
