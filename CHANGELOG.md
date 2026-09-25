# Changelog
All notable changes to this project will be documented in this file.

The format is based on [Keep a
Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic
Versioning](https://semver.org/spec/v2.0.0.html).

# [2.6.0] - 2026-09-24
This version includes changes to the template files, run `papyri` with `--copytemplate` at least once.
### Fixed
- web map links now restore the full view: position, zoom, dimension and enabled overlays (restoring a link used to drop the region grid and could leave the dimension out of sync with the layers control)
### Removed
- leaflet-fullHash plugin, replaced with a small inline URL hash sync using the same link format, so existing links keep working

# [2.5.0] - 2026-08-27
### Added
- support for the Minecraft 26.1+ world layout: maps are read from `data/minecraft/maps/<id>.dat` with `last_id.dat` as the marker
- warning when more than one world is found under the given path, naming the one whose maps are used
### Changed
- pre-26.1 worlds (`data/map_<id>.dat` with `idcounts.dat`) are still detected, the layout is picked per world folder
- progress bar label is now `*.dat -> nbt`, since map files are no longer all named `map_*.dat`

# [2.4.0] - 2026-06-30
This version includes changes to the template files, run `papyri` with `--copytemplate` at least once.
### Added
- web map search now covers banner names and every map ID at once, regardless of which overlays are shown; selecting a result enables its overlay and zooms to fit it (whole map polygon, or the banner location)
### Changed
- map results are listed as "map ID xxx" in the search box
- banner labels are centered under the banner icon
### Fixed
- browser no longer serves a stale cached copy of the inline web map code (added a no-cache header to `index.html`)

# [2.3.0] - 2026-06-30
This version includes changes to the template files, run `papyri` with `--copytemplate` at least once.
### Added
- faint grid on the web map aligned to the .mca region files (512x512), drawn beneath every layer and aligned to the mouse-position coordinates
- map panning and the region grid are limited to the Minecraft world border (configurable via the `WORLD_BORDER` constant in the template)
### Changed
- all web map dependencies are now vendored locally — no runtime CDN requests, fully offline
- updated Leaflet 1.4.0 -> 1.9.4, leaflet.markercluster 1.4.1 -> 1.5.3, leaflet-search -> 4.0.0
- pinned leaflet-pip to 1.1.0 (was loaded unpinned as `@latest`)
### Removed
- L.Control.MousePosition plugin, replaced with a small inline control showing block/chunk/region coords

# [2.2.0] - 2026-06-30
### Added
- custom GeoJSON overlays via an `overlays.json` manifest
### Changed
- modernized web map JS (fetch/async, module-scoped vars)
### Fixed
- selected overlays are preserved when switching dimensions

# [2.1.1] - 2025-11-24
### Fixed
- banner name skipping old data versions

# [2.1] - 2025-11-23
This version includes changes to the tempalte files, run `papyri` with `--copytemplate` at least once.
### Added
- search on web GUI
- home button on web GUI
- banner overlay enabled by default

# [2.0.6] - 2024-06-22
### Fixed
- fix for #46
- no longer supports bedrock
- fixes for other changes to map data over the years
- shimmed in #45 and #43, thank you @rm20killer and @LannyRipple

# [2.0.6] - 2022-03-19
### Fixed
- fix for #39

# [2.0.5] - 2020-08-29
### Fixed
- fix for #37 and 1.17 in general. New colors were added.

# [2.0.4] - 2020-02-09
### Added
- `--disablezoomsort` to skip sorting by zoom level, only by updated time #34

# [2.0.3] - 2020-12-19
### Fixed
- exact same banners are shown on map #30
- filename character issue for Windows #26
### Changed
- proper '#!' header

# [2.0.2] - 2020-12-07
### Fixed
- Logic surrounding selecting maps to render
- Removed extraneous console.log()s in index.html

# [2.0.1]
### Fixed
- wrong maps getting rendered

## [2.0]
This version changes the naming convention of the intermediate files created
in the output folder. A file called `1to2.sh` is included as a guide for renaming
the files if you'd like to preserve them. Otherwise, I recommend starting with
a fresh output folder.

### Added
- Maps now displayed in popup, this allows old maps and locked maps to have a
  place in papyri. Inspired by the Hermiton Herald.
- CHANGELOG
- Logo
- support for 1.16 and custom dimensions
### Fixed
- Windows path issues #21
- Slightly better support for modded servers #18
### Changed
- using NEAREST filter to keep pixelated Minecraft feel in some cases
  [@AndrewKvalheim](https://github.com/AndrewKvalheim)
- changed stylesheet to keep map pixelated at low zoom levels [@AndrewKvalheim](https://github.com/AndrewKvalheim)
- revamped intermediate file naming to support other features

## [1.0.0] - 2020-01-23
### Added
- Now using leaflet and a new tile rendering engine
- lots of performance improvements
### Removed
- dependency on vips and openseadragon
### Fixed
- Windows fixes [@TimoMeijer](https://github.com/TimoMeijer)
- Docker support [@TimoMeijer](https://github.com/TimoMeijer)

## [0.8.4] - 2018-10-14
### Added
- grid overlay
- spawn chunks overlay
- player overlay
- soring maps by time

## [0.8.3] - 2018-10-12
### Added
- mca file display
### Changed
- more pixelation to keep the Minecraft feel 
## [0.8.2] - 2018-10-11
### Added
- sort by map ID
- banner icons
- option to include unlimitedtracking
- live coords

## [0.8.0] - 2018-10-03
### Removed
- mdwiki generation
- book pois

## [0.7.0] - 2018-03-21
### Removed
- mdwiki in template

## [0.6.0] - 2018-03-07
### Added
- banner POIs
- MIT license

## [0.5.0] - 2018-02-24
### Changed
- increased size of possible rendered map

## [0.3.0] - 2018-02-03
### Added
- map ID overlay
- map statistics

## [0.2.0] - 2018-01-23
### Added
- customize POI colors
### Changed
- prepare for 1.13 book nbt/json changes

## [0.1.0] - 2018-01-07
### Added
- logging
- Books as POI

## [0.0.0] - 2018-01-06
### Added
- Initial commit
