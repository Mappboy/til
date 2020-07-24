---
categories:
- SPARQL
- RDF
date: "15-07-2020"
tags:
- wikipedia
- programming
slug: my-first-sparql-wikipedia
title: Querying wikipedia my first queries
---

I've always wanted to query with SQARQL but for some reason I always assumed it was quite hard.
Which it is coming from purely SQL background. 
However once you have the syntax down, and learn the shortcuts in the Wikidata editor it's not so hard.

Best tip is to use <kbd>CTRL</kbd> + <kbd>SPACE</kbd> to autofill your properties. I spent too long looking at wikipedia page
information before learning to use it.

Here's some quick queries.
 

__All universities__
```sparql
SELECT DISTINCT ?uni ?ranking ?coordinate_location WHERE {
  ?uni (wdt:P31/(wdt:P279*)) wd:Q3918.
  SERVICE wikibase:label { bd:serviceParam wikibase:language "[AUTO_LANGUAGE],en". }
  OPTIONAL { ?uni wdt:P625 ?coordinate_location. }
  OPTIONAL { ?uni wdt:P1352 ?ranking. }
  
}
ORDER BY DESC (?pr)
```

Get African countries currency, population, geography, and official languages
```sparql
SELECT DISTINCT ?country ?countryLabel ?currencyLabel ?population (GROUP_CONCAT(?offLangLabel; SEPARATOR = ",") AS ?off_langs) ?geo  WHERE {
  ?country (wdt:P31/wdt:P279) wd:Q6256;
    #wdt:P17 wd:Q114;
    wdt:P30 wd:Q15;
    wdt:P38 ?currency;
    wdt:P3896 ?geo;
    wdt:P1082 ?population.

    OPTIONAL {
    ?country wdt:P37 ?offLang.
}
  SERVICE wikibase:label {
    bd:serviceParam wikibase:language "[AUTO_LANGUAGE],en".
    ?country rdfs:label ?countryLabel.
    ?currency rdfs:label ?currencyLabel.
    ?offLang rdfs:label ?offLangLabel.
  }
}
GROUP BY ?country ?countryLabel ?currency ?currencyLabel ?population ?geo
ORDER BY ?country ?countryLabel ?currencyLabel ?population
```
## Further information
https://www.wikidata.org/wiki/Wikidata:SPARQL_query_service/Wikidata_Query_Help
https://www.wikidata.org/wiki/Wikidata:SPARQL_tutorial

##Python tools
https://people.wikimedia.org/~bearloga/notes/wdqs-python.html
https://pypi.org/project/sparql-client/
https://qwikidata.readthedocs.io/en/stable/readme.html
https://github.com/siznax/wptools
