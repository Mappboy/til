---
categories:
- GIS
- OSM
date: "15-07-2020"
tags:
- programming
- gis
title: OSM data downloads
---

```
# OSMTools tool require these packages. On Debian/Ubuntu you can install them with
sudo apt install graphviz sqlite3 aria2 osmctools

# install the package directly from git
python3 -m pip install git+https://github.com/openmaptiles/openmaptiles-tools

download-osm geofabrik rwanda-latest.osm.pbf

osmconvert rwanda-latest.osm.pbf --out-o5m > rwanda.o5m
osmfilter rwanda.o5m --keep="amenity=school name=" > rwanda_schools.o5m

# multipolygons and points layers
```