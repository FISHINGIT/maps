# AT Event Locations Map

Interactive maps visualising Angling Trust (AT) fishing event locations across England for 2025–26, overlaid with Environment Agency (EA) area boundaries.

## Files

| File | Description |
|------|-------------|
| `AT_event_locations_with_EA_areas.html` | Interactive map of AT event locations with EA area overlays |
| `AT_event_locations_with_EA_areas_UPDATED.html` | Updated version of the above map |
| `AT_map_D2_github_friendly.html` | Map variant D2, optimised for GitHub Pages hosting |
| `AT_map_option_A_light_clustering.html` | Map with light marker clustering (Option A) |
| `AT_map_option_D2_markers_obvious.html` | Map with prominent markers (Option D2) |
| `AT_map_github_pack.zip` | Packaged map files for distribution |
| `AT_events_2025-26_points.geojson` | GeoJSON point data for all AT events (2025–26) |
| `EA_areas.geojson` | GeoJSON polygons for Environment Agency areas |

## Data

The event data (`AT_events_2025-26_points.geojson`) includes:

- **event_name** – Full event name and venue
- **event_type** – e.g. Get Fishing, Get Fishing Awards
- **event_date** – Date of the event
- **region** – EA region code (e.g. SE, EE, YH)
- **postcode** – Venue postcode
- **attendees_rows** – Number of attendee rows recorded

## Built With

- [Folium](https://python-visualization.github.io/folium/) – Python library for Leaflet.js maps
- [Leaflet.js](https://leafletjs.com/) – Interactive map rendering
- [Leaflet.markercluster](https://github.com/Leaflet/Leaflet.markercluster) – Marker clustering
