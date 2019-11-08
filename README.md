# clics3

This repository contains 
- specifications of the source data,
- instructions to compile the CLICS database and
- the CLICS data as
  - (zipped) SQLite database
  - GML encoded network


## Creating the CLICS database

1. Install the Python package `pyclics`:
   ```shell script
   pip install "pyclics>=3.0"
   ```
2. Download and install the Lexibank datasets from which to aggregate colexifications:
   ```shell script
   pip install -r datasets.txt
   ```
3. Download data for the reference catalogs Glottolog and Concepticon:
   ```shell script
   cldfbench catconfig
   ```
4. Create the SQLite database:
   ```shell script
   clics load --glottolog-version v4.0 --concepticon-version v2.2.0
   ```
5. Create the colexification network (encoded as GML graph):
   ```shell script
   clics -t 3 -f families colexification
   clics -t 3 cluster infomap
   clics -t 3 -g infomap -f families graph_stats
   ```
