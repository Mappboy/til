---
categories:
- GIS
- OSM
date: 2020-07-15
tags:
- programming
- gis
slug: "osm-data-downloads"
title: OSM data downloads
---
Downloading OSM large data extracts is seriously easy.
```
# OSMTools tool require these packages. On Debian/Ubuntu you can install them with
sudo apt install graphviz sqlite3 aria2 osmctools

# install the package directly from git
python3 -m pip install git+https://github.com/openmaptiles/openmaptiles-tools

# Download a country dataset 
download-osm geofabrik africa/rwanda

# Filter out node's we want in this case schools
# o5m (fast binary) runs faster apparently could save the extra reconvert  
osmconvert rwanda-latest.osm.pbf --out-o5m > rwanda.o5m
osmfilter rwanda.o5m --keep="amenity=school and name!=None" > rwanda_schools.o5m
osmconvert rwanda_schools.o5m --out-osm > rwanda_schools.osm

# multipolygons and points layers quick import to postgres :) 
osm2pgsql --slim --username cam --database alu rwanda_schools.osm
```
