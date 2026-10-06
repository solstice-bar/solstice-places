# solstice-places

Generated data for [Solstice](https://solstice.bar) — every named café, restaurant and bar from
OpenStreetMap, with whether it has a terrace, cut into map tiles the app downloads for the area on
screen. Nothing here is edited by hand: the whole branch is rebuilt and replaced by an automated
job each month.

## Licence and attribution

The data is derived from OpenStreetMap and is available under the
[Open Database License (ODbL) 1.0](https://opendatacommons.org/licenses/odbl/1-0/).
**© OpenStreetMap contributors.** Any use must keep that attribution.

## Layout

```
v1/index.json          tiles present, their counts, the source extracts and their dates
v1/10/{x}/{y}.json     the places in one zoom-10 slippy-map tile
```

Each place is a positional array
`[id, name, lng, lat, amenity, terrace, cuisine, opening_hours, street, postcode, city, horizon?]`,
described in `v1/index.json`. `id` is the OSM object (`n123`, `w456`, `r789`); `terrace` is
`0` none, `1` confirmed, `2` unknown.

`horizon`, when present, is the skyline around the place: for each of 72 bearings (every 5°,
clockwise from north), the altitude in whole degrees above which the sky is clear within 500 m,
as two hex digits. Computed from OpenStreetMap buildings — `height`, else `building:levels` ×
3.1 m, else the median of tagged neighbours — so it inherits OSM's coverage of buildings.
