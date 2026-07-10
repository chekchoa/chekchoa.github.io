To update `plat-data.json` follow these steps;

1. Get the data using the following `GET` request:
`https://mapd.kcmo.org/kcgis/rest/services/DataLayers/MapServer/38/query?f=json&where=LEGAL%20like%20%27CARRIAGE%20HILL%25%20ESTATES%25%27&returnGeometry=false&spatialRel=esriSpatialRelIntersects&outFields=*&callback=`
2. Filter the `JSON` returned by the request using the following `jq` statement
`[.features[].attributes] | map({ city_pin: .KIVAPIN, county_apn: (.APN[2:]), platname: .PLATNAME, lot: .LOT, block: .BLOCK, legal_description: .LEGAL, address: (.ADDRESS | ascii_upcase), owners: .OWN_NAME}) | sort_by(.platname, .block, .lot)` 
