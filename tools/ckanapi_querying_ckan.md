---
categories:
- CKAN
- tools
date: 2020-07-29
tags:
- data
- query
- ckan
slug: ckanapi
title: Querying CKAN resources with ckanapi
---
Many government portals use CKAN for Open Data resources.
With [ckanapi](https://github.com/ckan/ckanapi) you can query them from the CMD line easily.

Here's a few little snippets.

```shell script
# Query all data with geospatial data.
ckanapi action package_search q=geodata -r https://data.gov.au/ | jq '.results| .[0]'

# Query groups with all fields
ckanapi action group_list all_fields=true -r https://data.gov.au/

# Get the number of datasets for each organization using KEY:JSON parameters
ckanapi action package_search facet.field:'["organization"]' rows:0 -r https://data.gov.au/
```

