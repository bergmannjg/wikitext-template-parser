# Wikitext Db Comparer

Compare wikitext [Route diagram](https://de.wikipedia.org/wiki/Wikipedia:Formatvorlage_Bahnstrecke) templates with [data](https://data.deutschebahn.com/dataset/geo-betriebsstelle) from Open-Data-Portal of Deutsche Bahn.

This is done in several steps.

## Extract route info in 'STRECKENNR' Template

The route number and start/stop stations of a route are given in the 'STRECKENNR' template parameter in multiple ways, for example:

```
1730 (Hannover–Lehrte)
6107 (Lehrte–Oebisfelde)
6185 (Oebisfelde–Berlin-Spandau)
```

To compare the routes it is necessary that the station names in the 'STRECKENNR' template correspond to the station names in the 'BS' templates. In some instances there is no direct correspondence.

## From Templates to StationsOfInfobox

All templates of an wiki info box with station data are extracted and transformed in StationOfInfobox type.

## From StationsOfInfobox to StationsOfRoute of a route

The stations of a route are filtered from the StationOfInfobox data with the RouteInfo and transformed in StationOfRoute type.

## Compare Wikitext Stations with DB Stations

Compare the wikitext station data of a route with the corresponding db data, i.e. are the stations in db data a subset of the stations in wiki data.

A wikitext station matches with a db station 

* if the distance differences are small 
* and the the staion names have a common substring.

### Usage

Usage example of comparer:

```
dotnet run --project src/WikitextDbComparer/WikitextDbComparer.fsproj -comparetitle Bahnstrecke_Nürnberg–Feucht
```

This give the follwoing output

```
{ route = 5970
  title = "Bahnstrecke_Nürnberg–Feucht"
  fromToName = [|"Nürnberg Hbf"; "Feucht"|]
  fromToKm = [|0.0; 12.5|]
  countWikiStops = 8
  countDbStops = 5
  countDbStopsNotFound = 0
  resultKind = WikidataFound }
```