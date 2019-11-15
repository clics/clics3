# CLICS³

The third installment of [CLICS](https://github.com/clics/clics) - the database of Cross-Linguistic Colexifications.

Cite as

> Rzymski, Tresoldi et al. 2019. The Database of Cross-Linguistic Colexifications, reproducible analysis of cross- linguistic polysemies. DOI: doi.org/10.17613/5awv-6w15

This repository contains 
- specifications of the source data as [human readable table](datasets.md) and as
  [requirements file to install with `pip`](datasets.txt)
- a map showing the geographic distribution of languages in the CLICS database,
  [encoded in GeoJSON](languoids.geojson)
- instructions to compile the CLICS database (see below) and
- the CLICS data:
  - the [(zipped) SQLite database](clics3.sqlite.zip) created in step 4 below, zipped running
    ```shell script
    zip -9 clics3.sqlite.zip clics.sqlite
    ```
  - the [full, GML encoded network](clics3-network.gml.zip) created in step 5 below, zipped running
    ```shell script
    zip -9 clics3-network.gml.zip graphs/network-3-families.gml
    ```
- the exact set of [`pip` requirements](requirements.txt) used to create the artefacts
  above.

This data is licensed under [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/).


## Creating the CLICS database

1. Install version 3 of the Python package `pyclics`
   [![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.3539050.svg)](https://doi.org/10.5281/zenodo.3539050):
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
4. Create the SQLite database `clics.sqlite`:
   ```shell script
   clics load --glottolog-version v4.0 --concepticon-version v2.2.0
   ```
   and confirm all 30 datasets have been loaded
   ```shell script
   clics datasets
   ```

| # | Dataset | Parameters | Concepticon | Varieties | Glottocodes | Families |
|:----|:------------------|-------------:|--------------:|------------:|--------------:|-----------:|
| 1 | abrahammonpa | 304 | 304 | 30 | 16 | 2 |
| 2 | allenbai | 499 | 499 | 9 | 9 | 1 |
| 3 | bantubvd | 420 | 415 | 10 | 10 | 1 |
| 4 | beidasinitic | 736 | 735 | 18 | 18 | 1 |
| 5 | bodtkhobwa | 553 | 536 | 8 | 8 | 1 |
| 6 | bowernpny | 338 | 338 | 175 | 172 | 1 |
| 7 | castrosui | 510 | 508 | 16 | 3 | 1 |
| 8 | chenhmongmien | 793 | 793 | 22 | 20 | 1 |
| 9 | diacl | 537 | 537 | 371 | 351 | 25 |
| 10 | halenepal | 699 | 662 | 13 | 13 | 2 |
| 11 | hantganbangime | 299 | 299 | 22 | 22 | 5 |
| 12 | hubercolumbian | 346 | 345 | 69 | 65 | 16 |
| 13 | ids | 1310 | 1308 | 320 | 275 | 60 |
| 14 | kraftchadic | 433 | 428 | 66 | 59 | 2 |
| 15 | lexirumah | 604 | 602 | 357 | 231 | 12 |
| 16 | logos | 707 | 707 | 5 | 5 | 1 |
| 17 | marrisonnaga | 580 | 572 | 40 | 39 | 1 |
| 18 | mitterhoferbena | 342 | 335 | 13 | 13 | 1 |
| 19 | naganorgyalrongic | 969 | 877 | 10 | 8 | 1 |
| 20 | northeuralex | 952 | 951 | 107 | 107 | 21 |
| 21 | robinsonap | 391 | 391 | 13 | 13 | 1 |
| 22 | satterthwaitetb | 418 | 418 | 18 | 18 | 1 |
| 23 | sohartmannchin | 279 | 279 | 8 | 7 | 1 |
| 24 | suntb | 929 | 929 | 49 | 49 | 1 |
| 25 | tls | 1140 | 811 | 126 | 107 | 1 |
| 26 | transnewguineaorg | 904 | 865 | 1004 | 760 | 106 |
| 27 | tryonsolomon | 317 | 314 | 111 | 96 | 5 |
| 28 | wold | 1459 | 1458 | 41 | 41 | 24 |
| 29 | yanglalo | 875 | 869 | 7 | 7 | 1 |
| 30 | zgraggenmadang | 311 | 310 | 98 | 98 | 1 |
| | TOTAL | 0 | 2906 | 3156 | 2271 | 200 |

5. Create the colexification network (encoded as GML graph):
   ```shell script
   clics -t 3 -f families colexification --show 20 --format pipe
   ```
   This will create the graph at `graphs/network-3-families.gml` and show the 20 most common colexifications:

| ID A | Concept A | ID B | Concept B | Families | Languages | Words |                                                                                                        
|-------:|:-------------------------|-------:|:-------------------------------|-----------:|------------:|--------:|
| 906 | TREE | 1803 | WOOD | 59 | 348 | 361 |
| 1313 | MOON | 1370 | MONTH | 57 | 324 | 327 |
| 72 | CLAW | 1258 | FINGERNAIL | 55 | 236 | 243 |
| 1297 | LEG | 1301 | FOOT | 52 | 349 | 358 |
| 1352 | KNIFE | 3210 | KNIFE (FOR EATING) | 51 | 268 | 282 |
| 2267 | SON-IN-LAW (OF MAN) | 2266 | SON-IN-LAW (OF WOMAN) | 49 | 261 | 280 |
| 763 | SKIN | 1204 | BARK | 49 | 209 | 213 |
| 1307 | LANGUAGE | 1599 | WORD | 49 | 148 | 149 |
| 1277 | HAND | 1673 | ARM | 48 | 294 | 300 |
| 1408 | HEAR | 1608 | LISTEN | 48 | 107 | 109 |
| 634 | MEAT | 2259 | FLESH | 47 | 252 | 262 |
| 2265 | DAUGHTER-IN-LAW (OF MAN) | 2264 | DAUGHTER-IN-LAW (OF WOMAN) | 47 | 234 | 256 |
| 763 | SKIN | 629 | LEATHER | 46 | 236 | 258 |
| 837 | BLUE | 1425 | GREEN | 46 | 195 | 204 |
| 2261 | MALE (OF PERSON) | 2263 | MALE (OF ANIMAL) | 45 | 145 | 163 |
| 1199 | WIFE | 962 | WOMAN | 44 | 289 | 301 |
| 480 | PLATE | 481 | DISH | 44 | 155 | 170 |
| 2260 | FEMALE (OF PERSON) | 2262 | FEMALE (OF ANIMAL) | 44 | 146 | 154 |
| 1228 | EARTH (SOIL) | 626 | LAND | 43 | 159 | 167 |
| 667 | ROAD | 2252 | PATH | 43 | 133 | 153 |
| 705 | GO UP (ASCEND) | 1102 | CLIMB | 43 | 132 | 146 |
| 683 | PERSON | 1554 | MAN | 41 | 199 | 205 |
| 2255 | FATHER-IN-LAW (OF MAN) | 2254 | FATHER-IN-LAW (OF WOMAN) | 41 | 187 | 204 |
| 133 | WEAVE | 3294 | BRAID (VERB) OR WEAVE (BASKET) | 41 | 122 | 133 |
| 2261 | MALE (OF PERSON) | 1554 | MAN | 41 | 104 | 115 |
| 1474 | SEA | 645 | OCEAN | 41 | 101 | 110 |
| 215 | LIE DOWN | 1585 | SLEEP | 40 | 191 | 197 |
| 1265 | HIGH | 711 | TALL | 40 | 168 | 182 |
| 256 | FOOD | 1526 | MEAL | 40 | 124 | 136 |
| 1732 | SKY | 1565 | HEAVEN | 40 | 117 | 120 |
| 1443 | WALK | 695 | GO | 39 | 288 | 320 |
| 2257 | MOTHER-IN-LAW (OF MAN) | 2256 | MOTHER-IN-LAW (OF WOMAN) | 39 | 181 | 203 |
| 1618 | GRANDSON | 1619 | GRANDDAUGHTER | 39 | 133 | 151 |
| 1203 | LONG | 711 | TALL | 39 | 113 | 121 |
| 2260 | FEMALE (OF PERSON) | 962 | WOMAN | 39 | 109 | 119 |
| 948 | WATER | 666 | RIVER | 38 | 197 | 200 |
| 1229 | OLD | 406 | OLD MAN | 38 | 103 | 107 |
| 531 | HOW MUCH | 3450 | HOW MANY PIECES | 37 | 184 | 203 |
| 706 | DARK | 163 | BLACK | 37 | 95 | 97 |
| 855 | SEIZE | 702 | CATCH | 36 | 150 | 161 |


6. Run subgraph and infomap cluster algorithms:
   ```shell script
   clics --seed 42 -t 3 -f families makeapp
   ```
   The clustered networks will be written to GML graphs and exported in a way suitable 
   for exploring with the CLICS javascript app. We can get some summary statistics running
   ```shell script
   clics -t 3 -f families --graphname infomap graph_stats
   -----------  ----
   nodes        1647
   edges        2967
   components     92
   communities   249
   -----------  ----
   ```
7. Finally, we can explore the clusters in the CLICS javascript app:
   ```shell script
   clics runapp
   ```

