# clics3

This repository contains 
- specifications of the source data,
- instructions to compile the CLICS database and
- the CLICS data as
  - (zipped) SQLite database
  - GML encoded network


## Creating the CLICS database

1. Install the Python package `pyclics` in versin 2.0:
   ```bash
   pip install "pyclics==2.0"
   ```
2. Download and install the Lexibank datasets from which to aggregate colexifications:
   ```bash
   pip install -r datasets.txt
   ```
3. Download data for the reference catalogs Glottolog and Concepticon:
   get concepticon-data and glottolog from zenodo!

4. Create the SQLite database:
   ```bash
   clics load path/to/concepticon-data path/to/glottolog
   ```
5. Create the colexification network (encoded as GML graph):
   ```bash
   clics -t 3 -f families colexification
   ```

