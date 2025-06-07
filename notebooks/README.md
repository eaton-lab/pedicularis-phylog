# Pedicularis phylogeography notebooks

* **map-HMR-basins.ipynb** - Plotting samples in the context of river basins in the region.
* **PyGDM-PrepData.ipynb** - Python notebook for doing all the data preparation
for running GDM.
* **R-GDM-V2.ipynb** (Requires R kernel) - R notebook which is only responsible
for running GDM. Reads in all the data prepped by the PyGDM notebook.

#### `_arch` directory contains deprecated notebooks
These may be useful in the future, but are archived for the moment,
superseded by other notebooks.
* PyGDM-rpy2-Dev.ipynb - An attempt to run the GDM R package inside a
python notebook with rpy2. Never worked, but I also gave up on it quickly.
* R-GDM-V1.ipynb - An early version of the R kernel notebook. There are
several ways to run GDM and I experimented with a few of them here before
settling on the site x species matrix approach. Perhaps useful to see these
if we need to change our approach at some point.
