# go-http-maps

Go package providing opinionated HTTP middleware for web-based map tiles.

## Important

This is work in progress. Documentation is incomplete.

Until then have a look at [app/server/server.go](app/server/server.go), [templates/html/map.html](templates/html/map.html) and [static/javascript/aaronland.map.init.js](static/javascript/aaronland.map.init.js) for an example of working code.

## tools

### server

An example HTTP server demonstrating the use of the `go-http-maps` package.

```
> ./bin/server -h
  -initial-latitude float
    	The starting latitude to position the map at. (default 37.61799)
  -initial-longitude float
    	The start longitude to position the map at. (default -122.370943)
  -initial-zoom int
    	The starting zoom level to position the map at. (default 12)
  -javascript-at-eof
    	An optional boolean flag to indicate that JavaScript resources (<script> tags) should be appended to the end of the HTML output.
  -leaflet-enable-draw
    	Enable the Leaflet.Draw plugin.
  -leaflet-enable-fullscreen
    	Enable the Leaflet.Fullscreen plugin.
  -leaflet-enable-hash
    	Enable the Leaflet.Hash plugin. (default true)
  -leaflet-tile-url string
    	A valid Leaflet 'tileLayer' layer URL. Only necessary if -map-provider is "leaflet".
  -map-prefix string
    	...
  -map-provider string
    	The name of the map provider to use. Valid options are: leaflet, null, protomaps
  -protomaps-bucket-uri string
    	The gocloud.dev/blob.Bucket URI where Protomaps tiles are stored. Only necessary if -map-provider is "protomaps" and -protomaps-serve-tiles is true.
  -protomaps-caches-size int
    	The size of the internal Protomaps cache if serving tiles locally. Only necessary if -map-provider is "protomaps" and -protomaps-serve-tiles is true. (default 64)
  -protomaps-database string
    	The name of the Protomaps database to serve tiles from. Only necessary if -map-provider is "protomaps" and -protomaps-serve-tiles is true.
  -protomaps-label-rules-uri gocloud.dev/runtimevar
    	// An optional gocloud.dev/runtimevar URI referencing a custom Javascript variable used to define Protomaps label rules.
  -protomaps-paint-rules-uri gocloud.dev/runtimevar
    	// An optional gocloud.dev/runtimevar URI referencing a custom Javascript variable used to define Protomaps paint rules.
  -protomaps-serve-tiles
    	A boolean flag signaling whether to serve Protomaps tiles locally. Only necessary if -map-provider is "protomaps".
  -protomaps-tile-url string
    	A valid Protomaps .pmtiles URL for loading map tiles. Only necessary if -map-provider is "protomaps". (default "/tiles/")
  -rollup-assets
    	An optional boolean flag to indicate that multiple JavaScript and CSS assets should be minified and combined in to single files.
  -server-uri string
    	A valid aaronland/go-http-server URI (default "http://localhost:8080")
```

### Example

#### protomaps

![](docs/images/http-maps-protomaps.png)

```
go run -mod vendor cmd/server/main.go \
	-map-provider protomaps \
	-protomaps-serve-tiles \
	-protomaps-bucket-uri file:///{PATH_TO}/go-http-maps/fixtures
	-protomaps-database sfo
```

#### leafet

![](docs/images/http-maps-leaflet.png)

```
go run -mod vendor cmd/server/main.go \
	-map-provider leaflet
	-leaflet-tile-url https://tile.openstreetmap.org/{z}/{x}/{y}.png
```

## See also

* https://github.com/aaronland/go-http-leaflet
* https://github.com/aaronland/go-http-protomaps
