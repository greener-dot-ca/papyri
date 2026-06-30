# papyri version 2.1

Papyri is a Java Minecraft map item web presenter. It will show all maps and banners created on a server positioned and scaled properly, creating a mosaic of your world as explored with maps. Since many maps can be created of the same area, Papyri will prioritize rendering so that maps with higher detail are rendered on top of maps of lower detail and maps at the same detail are rendered in order from oldest updated to newest updated.

[Example - Barlynaland](https://barlynaland.minecraft.greener.ca/)

![Papyri](logo.png)

## Setup environment

```
python3 -m venv venv
./venv/bin/pip install -r requirements.txt
source ./venv/bin/activate
```


Remember to read [CHANGELOG.md](CHANGELOG.md) for important info on releases.

## usage

```
usage: papyri.py [-h] --world WORLD --type {java,bds}
                 [--includeunlimitedtracking] --output OUTPUT [--copytemplate]
                 [--debug]

convert minecraft maps to the web

optional arguments:
  -h, --help            show this help message and exit
  --world WORLD         location of your world folder or save folder
  --includeunlimitedtracking
                        include maps that have unlimited tracking on, this
                        includes older maps from previous Minecraft versions
                        and treasure maps in +1.13
  --disablezoomsort     don't sort maps by zoom level before rendering, newer maps of higher zoom level will cover lower level maps
  --output OUTPUT       output path for web stuff
  --copytemplate        copy default index.html and assets (do this if a new
                        release changes the tempalte)
  --debug               show debug logging
```

Once it's done, the contents of the output folder can be served as a website. It's completely static so it can be put in an S3 bucket a github project or hosted locally on your machine by running something like `python3 -m http.server` inside the output folder.

## Custom Overlays

You can add custom GeoJSON overlays to your map by creating an `overlays.json` manifest file in your output folder:

```json
{
    "overlays": [
        "custom.json",
        "roads.json",
        "points-of-interest.json"
    ]
}
```

Each file listed in the manifest should be a JSON array of GeoJSON features with a `dimension` property:

```json
[
    {
        "type": "Feature",
        "geometry": {
            "type": "LineString",
            "coordinates": [[0, 0], [100, 100]]
        },
        "properties": {
            "dimension": "minecraft@overworld",
            "style": {
                "color": "#ff0000",
                "weight": 2
            }
        }
    }
]
```

- Overlay files are loaded in parallel for performance
- If `overlays.json` doesn't exist, custom overlays are skipped silently
- If an individual overlay file fails to load, a warning is logged but other overlays continue loading

## Region grid

The web map draws a faint grid aligned to Minecraft's `.mca` region files (one line every 512 blocks). It sits beneath every other layer, so it only shows through where the map hasn't been rendered yet, and it lines up exactly with the X/Z coordinates shown in the mouse-position readout.

Both the grid and map panning are limited to the bounds of a Minecraft world (the default world border, ±29,999,984 blocks from origin). If your server uses a different world border, change the `WORLD_BORDER` constant near the top of the template's `index.html`.

This project is licensed under the terms of the MIT license.
