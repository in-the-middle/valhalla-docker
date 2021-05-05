## Environment variables

- `tile_urls`: Space-separated tiles URLs, e.g. https://download.geofabrik.de/europe/andorra-latest.osm.pbf http://download.geofabrik.de/europe/faroe-islands-latest.osm.pbf. Default `""`.
- `min_x`: Minimum longitude for elevation tiles, in decimal WGS84, e.g. 18.5
- `min_y`: Minimum latitude for elevation tiles, in decimal WGS84, e.g. 18.5
- `max_x`: Maximum longitude for elevation tiles, in decimal WGS84, e.g. 18.5
- `max_y`: Maximum latitude for elevation tiles, in decimal WGS84, e.g. 18.5
- `use_tiles_ignore_pbf`: `True` uses a local tile.tar file and skips building. Default `False`.
- `force_rebuild`: `True` forces a rebuild of the routing tiles. Default `False`.
- `build_elevation`: `True` builds elevation for the set coordinates. `Force` will do the same, but first delete any existing elevation tiles. Default `False`.
- `build_admins`: `True` builds the admin db. `Force` will do the same, but first delete the existing db. Default `False`.
- `build_time_zones`: `True` builds the timezone db. `Force` will do the same, but first delete the existing db. Default `False`.
- `server_threads`: How many threads `valhalla_service` will run with. Default is 1 thread less than the value of `nproc`.

#### Customize Valhalla configuration

If you need to customize Valhalla's configuration to e.g. increase the allowed maximum distance for the `/route` POST endpoint, just edit `custom_files/valhalla.json` and restart the container. It won't rebuild the tiles in this case, unless you tell it to do so via environment variables.

#### Run Valhalla with pre-built tiles

In the case where you have a pre-built `valhalla_tiles.tar` package from another Valhalla instance, you can also dump that to `custom_files/` and they're loaded upon container restart if you set the following environment variables: `use_tiles_ignore_pbf=True`, `force_rebuild=False`. Also, don't forget to set the md5 sum for your `valhalla_tiles.tar` in `.file_hashes.txt`.
