# destination-mapbox
A Brandwatch Vizia destination to render volume data using [Mapbox GL JS][mb] maps and [D3][d3]

## Demo
To run the demo run `npm start` and point your browser to the suggested url.


## The EU data

### Included countries list (Alpha 3 codes):

`'ALA', 'ALB', 'AND', 'ARM', 'AUT', 'BEL', 'BGR', 'BIH', 'BLR', 'CHE', 'CYP', 'CZE', 'DEU', 'DNK', 'ESP', 'EST', 'FIN', 'FRA', 'FRO', 'GBR', 'GGY', 'GIB', 'GRC', 'HRV', 'HUN', 'IMN', 'IRL', 'ISL', 'ITA', 'JEY', 'LIE', 'LTU', 'LUX', 'LVA', 'MCO', 'MDA', 'MKD', 'MLT', 'MNE', 'NLD', 'NOR', 'POL', 'PRT', 'ROU', 'SMR', 'SRB', 'SVK', 'SVN', 'SWE', 'TUR', 'UKR', 'UNK', 'VAT'`

### Omitted countries list (Alpha 3 codes):

The following countries which are often considered to be part of Europe have been omitted as they are not part of what the Brandwatch API returns when using the `eu` location filter:

`'AZE', 'GEO', 'KAZ', 'RUS'`


## The APAC data

### Included countries list (Alpha 3 codes):

`AUS', 'BGD', 'BTN', 'IOT', 'BRN', 'KHM', 'CHN', 'HKG', 'IND', 'IDN', 'JPN', 'PRK', 'KOR', 'LAO', 'MAC', 'MDV', 'MYS', 'MNG', 'MMR', 'NPL', 'NZL', 'PAK', 'PNG', 'PHL', 'PHL', 'SGP', 'LKA', 'TWN', 'THA', 'TLS', 'VNM'`

### Included countries list (Alpha 2 codes):

`'AU', 'BD', 'BT', 'IO', 'BN', 'KH', 'CN', 'HK', 'IN', 'ID', 'JP', 'KP', 'KR', 'LA', 'MO', 'MV', 'MY', 'MN', 'MM', 'NP', 'NZ', 'PK', 'SG', 'LK', 'TW', 'TL', 'VN'`


## Making the maps

These sample commands are based around the EU map but are also valid for the APAC map.

To manipulate the shape files install GDAL with the following command:

`brew install gdal`

TopoJSON can be installed with the following command:

`npm install -g topojson`

### Converting the data from shape file to GeoJSON

The following command will generate a `subunits.json` GeoJSON map for all the countries in the list that match the `ADM0_A3` property:

`ogr2ogr  -f GeoJSON  -where "ADM0_A3 IN ('ALA', 'ALB', 'AND', 'ARM', 'AUT', 'BEL', 'BGR', 'BIH', 'BLR', 'CHE', 'CYP', 'CZE', 'DEU', 'DNK', 'ESP', 'EST', 'FIN', 'FRA', 'FRO', 'GBR', 'GGY', 'GIB', 'GRC', 'HRV', 'HUN', 'IMN', 'IRL', 'ISL', 'ITA', 'JEY', 'LIE', 'LTU', 'LUX', 'LVA', 'MCO', 'MDA', 'MKD', 'MLT', 'MNE', 'NLD', 'NOR', 'POL', 'PRT', 'ROU', 'SMR', 'SRB', 'SVK', 'SVN', 'SWE', 'TUR', 'UKR', 'UNK', 'VAT')"  subunits.json  ne_10m_admin_0_map_subunits.shp`


If we wanted to add some points for the major cities (i.e. like in the vizia.old d3 globe) we could use something like the command below. This generates a `places.json` GeoJSON file for all the countries in the list that match the `ISO_A2` property. The `ISO_A2` format is used here instead of the `ADM0_A3` because the populated places shape file only provides data in this format.

`ogr2ogr  -f GeoJSON  -where "ISO_A2 IN ('PT', 'ES', 'IE', 'IS', 'GB', 'AD', 'FO', 'FR', 'BE', 'MC', 'LU', 'CH', 'NL', 'DK', 'DE', 'NO', 'FL', 'VA', 'SM', 'IT', 'AT', 'SE', 'SI', 'CZ', 'HR', 'BA', 'MT', 'PL', 'HU', 'SK', 'ME', 'LT', 'LV', 'FI', 'AL', 'RS', 'XK', 'EE', 'MK', 'GR', 'RO', 'BG', 'BY', 'MD', 'UA') AND SCALERANK < 5"  places.json  ne_10m_populated_places.shp`

All the above command assumes that you have unzipped the `ne_10m_admin_0_map_subunits.zip` in your directory.

### Converting the GeoJSON map to TopoJSON

From the [topojson repository][tr]:

>TopoJSON is an extension of GeoJSON that encodes topology. Rather than representing geometries discretely, geometries in TopoJSON files are stitched together from shared line segments called arcs. TopoJSON eliminates redundancy, offering much more compact representations of geometry than with GeoJSON; typical TopoJSON files are 80% smaller than their GeoJSON equivalents.

The following command will generate a `eu.json` TopoJSON map starting from the `subunits.json` map created previously. `ADMIN` is the chosen property to promote to geometry `id` and only the `NAME` property is being plucked for each country, this is also being renamed to `name`.

`topojson -o eu.json --id-property ADMIN -p name=NAME -- subunits.json`

N.B. This commands are valid for the v1.x of topojson, I'll hopefully update these soon to support v2.x.

## Merging the population, population density and bounding box data with the TopoJSON map

To update a topojson map with new metadata coming from a CSV/TSV (the only supported formats) run the following:

`topojson -o eu-with-metadata.json -e eu-metadata.csv --id-property=name -p -- eu.json`

See the topojson CLI [documentation][topodocs] for a detailed explaination of the various flags. The `--id-property` is the name of the GeoJSON feature property to promote to geometry `id` which is also used to join the data coming in from the CSV/TSV.


## Data Sources:

Shape files and other GIS data:
* [Natural Earth 1:10m cultural vectors][ne]

ISO-3166 country codes:
* [Alpha 2][a2]
* [Alpha 3][a3]

Population and population density data (km<sup>2</sup>):
* [EU][eu]
* [APAC][apac]
* [Turkey][tu]

Bounding boxes:
* [GeoPlanet][gp]
* [Bounding Box Tool][bbt]

Colour scales:
* [MPL Colormaps][mpl]

### Known Issues

Unfortunately the resulting map is often not going to work right away and will need a bit of manual clean up. I believe there are some GDAL commands that should solve some of these issues but for the time being here's a list of the manual enchanments I had to do in orider to produce the final EU/APAC map. Look away now!

### EU Issues

* Merge the territories (Polygons/MultiPolygons arcs) for the following countries: Bosnia and Herzegovina, Denmark (do not to include the Faroe Islands), Spain, France, Guernsey, Italy, Norway, Serbia
* Generate (as there is no ADM0_A3 entry for) Belgium from merging the 3 separate territories
* Generate (as there is no ADM0_A3 entry for) the United Kingdom from merging the 4 separate territories, making sure not to include Guernsey, Gibraltar, the Isle of Man and Jersey.
* Rename `Fed. of Bos. & Herz.` -> `Bosnia and Herzegovina`
* Rename `Czech Rep.` -> `Czech Republic`
* Rename `Faeroe Is.` -> `Faeroe Is.` to `Faroe Islands`
* Rename `Vatican` -> `Vatican City`
* Rename `Ireland` -> `Republic of Ireland`
* Rename `Macedonia` -> `Republic of Macedonia`

### APAC Issues
* Merge the territories (Polygons/MultiPolygons arcs) for the following countries: Australia, China, India, British Indian Ocean Territory, Japan, South Korea, North Korea, New Zealand, Papua New Guinea and East Timor
* Merge `Macao` with `China` as it is not an independent terriory in the Brandwatch API
* Rename `China` -> `People's Republic of China`
* Rename `Cambodia` -> `Cambodia Khmer`
* Rename `South Korea` -> `Republic of Korea`
* Rename `North Korea` -> `Democratic People's Republic of Korea`
* Rename `Timor-Leste` - `East Timor`
* Rename `Taiwan` -> `Republic of China (Taiwan)`

## Data Normalisation

At the moment, there are three options for the values to use in choropleth maps (specified with the URL `metric` argument):
* `value`: raw mention volume per area,
* `valuePopulationNormal`: mention volume over population by area - with a relative indicator between -100 and 100 for figure,
* `valuePopulationSmooth`: Empirical Bayes smoothing (implementation details from [here][ebs]) applied to mention volume over population by area - also with a relative figure between -100 and 100.


[mb]: https://github.com/mapbox/mapbox-gl-js
[d3]: https://github.com/d3/d3
[ne]: http://www.naturalearthdata.com/downloads/10m-cultural-vectors/
[a2]: https://en.wikipedia.org/wiki/ISO_3166-1_alpha-2
[a3]: https://en.wikipedia.org/wiki/ISO_3166-1_alpha-3
[apac]: https://en.wikipedia.org/wiki/Asia-Pacific#Main_countries_and_territories_data
[eu]: https://en.wikipedia.org/wiki/Area_and_population_of_European_countries
[tu]: https://en.wikipedia.org/wiki/Turkey
[gp]: http://isithackday.com/geoplanet-explorer/
[bbt]: http://boundingbox.klokantech.com/
[tr]: https://github.com/mbostock/topojson
[topodocs]: https://github.com/mbostock/topojson/wiki/Command-Line-Reference/
[mpl]: https://bids.github.io/colormap/
[ebs]: http://www.dpi.inpe.br/gilberto/tutorials/software/geoda/tutorials/w6_rates_slides.pdf
