# CLAUDE.md — Repository Guide for AI Assistants

## Project Overview

This repository contains two distinct components:

1. **Angling Trust Event Maps** — Interactive Leaflet.js maps visualising Angling Trust (AT) fishing events across England (2025–26 season), overlaid with Environment Agency (EA) administrative boundaries.
2. **Growth OS for Claude Cowork Quick Start Plugin** — A Claude Cowork plugin that guides users through setting up an AI-powered business workspace.

There is no build system, package manager, or server-side code. All map files are self-contained static HTML or load external GeoJSON from the same directory.

---

## Repository Structure

```
maps/
├── # Map HTML files
├── AT_map_D2_github_friendly.html          # Recommended: lightweight, loads GeoJSON externally
├── AT_map_option_A_light_clustering.html   # Self-contained, light clustering style
├── AT_map_option_D2_markers_obvious.html   # Self-contained, prominent markers style
├── AT_event_locations_with_EA_areas.html   # Original self-contained version
├── AT_event_locations_with_EA_areas_UPDATED.html  # Updated self-contained version
│
├── # GeoJSON data files (loaded by AT_map_D2_github_friendly.html at runtime)
├── AT_events_2025-26_points.geojson        # 240 AT fishing events (points)
├── EA_areas.geojson                        # 14 Environment Agency operational areas (polygons)
│
├── # Archived assets
├── AT_map_github_pack.zip                  # Zip of github-friendly map + GeoJSON files
│
├── # Claude Cowork plugin files
├── plugin.json                             # Plugin metadata (name, version, author)
├── quick-start.md                          # Slash-command definition for /quick-start
├── README.md                               # Plugin documentation
├── gOS-claude-cowork-quick-start-v1.0.0.zip  # Plugin distribution archive
```

---

## Component 1: Angling Trust Event Maps

### Technology Stack

- **Leaflet.js** — Interactive map rendering (v1.9.4 in the github-friendly file; v1.x via cdnjs in self-contained files)
- **Leaflet.markercluster** — Cluster grouping of event markers
- **OpenStreetMap** — Tile layer provider
- **GeoJSON** — Data format for both events and EA areas
- **Pure vanilla JavaScript** — No frameworks or build tools
- **CDN-hosted dependencies** — No local npm packages

### Map Variants

| File | Data loading | Intended use |
|------|-------------|--------------|
| `AT_map_D2_github_friendly.html` | Fetches `EA_areas.geojson` and `AT_events_2025-26_points.geojson` at runtime via `fetch()` | GitHub Pages deployment — recommended |
| `AT_map_option_A_light_clustering.html` | GeoJSON embedded inline in the HTML | Self-contained sharing (email, local file) |
| `AT_map_option_D2_markers_obvious.html` | GeoJSON embedded inline in the HTML | Self-contained, alternative marker style |
| `AT_event_locations_with_EA_areas.html` | GeoJSON embedded inline in the HTML | Original version |
| `AT_event_locations_with_EA_areas_UPDATED.html` | GeoJSON embedded inline in the HTML | Updated original version |

**The github-friendly file is the canonical lightweight version.** The self-contained files are large (23–26 MB each) because they embed all GeoJSON data inline.

### GeoJSON Data Schema

**`AT_events_2025-26_points.geojson`** — 240 features, geometry type: `Point`

| Property | Type | Description |
|----------|------|-------------|
| `event_name` | string | Full event name and location |
| `event_type` | string | `"Get Fishing"`, `"Get Fishing Awards"`, `"Get Fishing Award"`, `"GHoF Get Fishing - Family Fishing"` |
| `event_date` | string | ISO 8601 date (`YYYY-MM-DD`), range: 2025-04-01 to 2025-12-06 |
| `region` | string | Region code: `EE`, `EM`, `NE`, `NW`, `SE`, `SW`, `WM`, `YH` |
| `postcode` | string | UK postcode |
| `source` | string | Always `"AT"` |
| `attendees_rows` | integer | Number of attendee rows in source data |

**`EA_areas.geojson`** — 14 features, geometry type: `Polygon`, CRS: EPSG:4326

| Property | Type | Description |
|----------|------|-------------|
| `OBJECTID` | integer | Unique ID |
| `LONG_NAME` | string | Full EA area name (e.g., `"Thames"`, `"Cumbria and Lancashire"`) |
| `SHORT_NAME` | string | Abbreviated name |
| `IDENTIFIER` | integer | EA area identifier |
| `CODE` | string | Short code (e.g., `"THM"`, `"CLA"`) |
| `DESCRIPTIO` | string | Description of the EA area's geographic focus |
| `DATE_FROM` | string | Activation date |
| `DATE_TO` | string or null | Deactivation date (`null` = still active) |

### Map Features (AT_map_D2_github_friendly.html)

- **Default view**: England, centred at `[52.7, -1.5]`, zoom level 6
- **Tile layer**: OpenStreetMap
- **Clustered layer**: Events grouped into orange cluster markers; clusters expand below zoom 8; `disableClusteringAtZoom: 8`
- **Individual layer**: Every event shown as a `circleMarker` (radius 4–5px, navy `#003366`)
- **EA boundaries**: GeoJSON polygon overlay, blue stroke (`#1f77ff`), 5% fill opacity; tooltips show area name
- **Layer control**: Users can toggle EA areas, clustered events, and individual events
- **Popups**: Show `event_name`, `event_date`, `event_type`, `region`, `postcode`, `attendees_rows`
- **Fit bounds**: Map auto-fits to all event markers on load

### Deployment

The `AT_map_D2_github_friendly.html` file is designed for **GitHub Pages**. The HTML file and both `.geojson` files must be in the **same directory** — the HTML uses relative paths to `fetch()` them.

The `AT_map_github_pack.zip` contains the github-friendly HTML and both GeoJSON files pre-packaged for deployment.

### Editing Guidelines for the Maps

- **Do not embed GeoJSON inline** in the github-friendly file — it must remain lightweight and load data via `fetch()`.
- **Maintain EPSG:4326** coordinate reference system for all GeoJSON.
- **Leaflet version**: Stick to v1.9.4 (CDN) unless explicitly upgrading.
- **No build step**: Edit HTML and GeoJSON directly. There is no transpilation, bundling, or minification.
- **Self-contained variants**: If editing embedded-data files, update the inline GeoJSON to match the source `.geojson` files.
- **Popup fields**: The `popupHtml()` function guards against missing properties — keep this pattern when adding new fields.
- **Coordinate order**: GeoJSON uses `[longitude, latitude]`; Leaflet uses `[latitude, longitude]` — do not confuse these.

### Adding or Updating Events

To update event data:
1. Edit `AT_events_2025-26_points.geojson` (the source of truth for the github-friendly map).
2. For self-contained variants, replace the embedded GeoJSON object in the `<script>` block.
3. Validate GeoJSON with a tool like geojsonlint.com before committing.
4. Coordinates are `[longitude, latitude]` in GeoJSON.

---

## Component 2: Growth OS for Claude Cowork Quick Start Plugin

### What It Is

A Claude Cowork plugin that walks users through a structured onboarding process to build an AI-powered business workspace ("Growth OS"). It produces core business documents and a daily morning routine.

### Plugin Files

**`plugin.json`** — Plugin metadata:
```json
{
  "name": "growth-os-for-claude-cowork-quick-start",
  "version": "1.0.0",
  "description": "...",
  "author": { "name": "theCLICK" },
  "keywords": ["growth-os", "marketing", "quick-start", "onboarding"]
}
```

**`quick-start.md`** — Defines the `/quick-start` slash command:
- `allowed-tools`: `Read, Write, Edit, WebSearch, WebFetch, Bash, AskUserQuestion`
- Reads the skill file from `${CLAUDE_PLUGIN_ROOT}/skills/quick-start/SKILL.md`
- Supports resuming via a `progress.md` file in the workspace root
- Accepts optional `resume` argument

**`README.md`** — End-user documentation covering installation, usage, required vs. optional tiers, multi-session support, and example output.

### Plugin Tiers

- **Tier 1 (Required)**: Offers document, Persona document, Morning Routine
- **Tier 2 (Optional)**: Business Info, Brand Voice, Brand Design, Content Rules

### Plugin Conventions

- Progress is tracked in `progress.md` in the workspace root.
- The skill file lives at `${CLAUDE_PLUGIN_ROOT}/skills/quick-start/SKILL.md` (not in this repo directly).
- The distribution archive is `gOS-claude-cowork-quick-start-v1.0.0.zip`.

---

## Git Workflow

- **Main branch**: `master` / `main`
- **Feature branches**: Follow the pattern `claude/<description>-<id>` (e.g., `claude/add-claude-documentation-mbQHn`)
- **Commit messages**: Descriptive; current history uses "Add files via upload" (improve on this)
- **No CI/CD configuration** is present in this repository

### Push Instructions

```bash
git push -u origin <branch-name>
```

Branches must start with `claude/` and end with the matching session ID, or push will fail with HTTP 403.

---

## Common Tasks

### View a map locally

Open any `.html` file in a browser. For the github-friendly version, you need a local HTTP server (due to `fetch()` CORS restrictions with `file://`):

```bash
python3 -m http.server 8000
# Then open http://localhost:8000/AT_map_D2_github_friendly.html
```

The self-contained `.html` files can be opened directly as `file://` without a server.

### Validate GeoJSON

```bash
python3 -c "
import json
with open('AT_events_2025-26_points.geojson') as f:
    data = json.load(f)
print(f'Valid GeoJSON. Features: {len(data[\"features\"])}')
"
```

### Check event data statistics

```bash
python3 -c "
import json
with open('AT_events_2025-26_points.geojson') as f:
    data = json.load(f)
features = data['features']
types = set(f['properties']['event_type'] for f in features)
regions = set(f['properties']['region'] for f in features)
print(f'Events: {len(features)}, Types: {sorted(types)}, Regions: {sorted(regions)}')
"
```

---

## Key Conventions

1. **No build system** — All files are edited directly. No `npm install`, no compilation.
2. **CDN dependencies** — Leaflet and MarkerCluster are loaded from `unpkg.com` or `cdnjs.cloudflare.com`. Pin versions explicitly.
3. **GeoJSON coordinate order** — Always `[longitude, latitude]` in GeoJSON; always `[latitude, longitude]` in Leaflet.
4. **EPSG:4326** — All spatial data uses WGS 84 geographic coordinates.
5. **Graceful error handling** — Map files show `alert()` with a helpful message if data files fail to load.
6. **Separation of concerns** — The github-friendly file is the deployment target; the self-contained files are for sharing/offline use.
7. **Plugin progress tracking** — The quick-start plugin tracks state in `progress.md` to support multi-session workflows.
