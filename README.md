# MAP 675 module-02

## Lis Fano and Matthew Bacinskas

### Curl command used to download all the TriMet zip files
`curl -Lk --remote-name-all https://developer.trimet.org/gis/data/{tm_boundary,tm_parkride,tm_rail_lines,tm_rail_stops,tm_routes,tm_stops,tm_route_stops,tm_tran_cen}.zip`

### Bash command used to unzip all of the downloaded zipped directories
`for i in *.zip; do unzip -d "${i%.zip}" $i; done`

### GDAL command to convert route shapefile to WGS84
`ogr2ogr tm_routes_4326.shp -t_srs "EPSG:4326" tm_routes.shp`

### GDAL commmand used to convert WGS84 route shapefile to GeoJSON
` ogr2ogr -f "GeoJSON" trimet_routes.json tm_routes_4326.shp`

### GDAL command to just filter out bus routes from the JSON file
`ogr2ogr -f "GeoJSON" -where "type='BUS'" trimet_routes_bus.json trimet_routes.json`

