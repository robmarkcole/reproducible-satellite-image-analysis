# Reproducible-satellite-image-analysis
Whilst there are many well written articles on performing satellite image analysis, it is often a frustrating experience trying to reproduce the analysis owing to lack of detail about the package environment or broken links to imagery. This repository seeks to demonstrate best practice for allowing reproducible analysis, by using Binder to host a perfect reproduction of the analysis environment, complete with required imagery data.

## Conda
Use a conda environment to isolate required packages, and write an `environment.yaml` file to allow Binder to recreate the environment. Conda makes installing packages such as Rasterio straightforward, handling installation of their C++ dependencies for you (GDAL!). Using Conda environments with Jupyter notebooks is a bit of a hassle, and we use https://github.com/Anaconda-Platform/nb_conda_kernels locally. [Read this](https://ipython.readthedocs.io/en/stable/install/kernel_install.html#kernels-for-different-environments) -> we are making an ipython kernel from our conda env (below `sat_img_env`) available in the base env (`base`) from where I normally run Jupyter.

```
# Setup our environment
(base) $ conda install nb_conda_kernels
(base) $ conda create --name sat_img_env python=3.6
(base) $ conda activate sat_img_env
(sat_img_env) $ conda install ipykernel

# Install dependencies
(sat_img_env) $ conda install -c conda-forge rasterio
(sat_img_env) $ conda install -c conda-forge scikit-learn

# Save our env environment
(sat_img_env) $ conda env export > environment.yml
```

I usually run Jupyter from my `base` env, and we need to make the env available. In a second terminal:
```
(base) $ python -m ipykernel install --user --name sat_img_env
(base) $ jupyter notebook
```

Select the `sat_img_env` env from the drop-down menu at `Kernel > Change kernel > sat_img_env`:

<p align="center">
<img src="https://github.com/robmarkcole/reproducible-satellite-image-analysis/blob/master/data/select_env.png" width="700">
</p>

You are now using the `sat_img_env` env and can start working. EXCEPT WE ARE NOT..

<p align="center">
<img src="https://github.com/robmarkcole/reproducible-satellite-image-analysis/blob/master/data/env_usage.png" width="1000">
</p>

## Data
Github allows large files to be uploaded, although these should be kept to a minimum. If more than a couple of satellite images are required for analysis, it is best to put them in a public S3 bucket. I typically put imagery in a `data` folder.

## References
* A good article on best practices in data science is [here](https://medium.com/data-science-in-practice/saving-the-environment-with-anaconda-ad68e603d8c5).
