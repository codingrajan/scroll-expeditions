# Scroll expeditions

Scroll-driven 3D flythroughs of real routes, built from public elevation and
satellite data and delivered as fast, embeddable web experiences.

**Live: [ebc-flythrough.pages.dev](https://ebc-flythrough.pages.dev)**

[![Everest Base Camp flythrough](https://ebc-flythrough.pages.dev/og/og-image-v5.jpg)](https://ebc-flythrough.pages.dev)

## The courses

### [Everest Base Camp](https://ebc-flythrough.pages.dev/ebc/)
The classic trek, Lukla to Base Camp — 62 km, 2,860 m to 5,364 m — rendered
from Copernicus elevation and Sentinel-2 imagery. Twelve hand-authored camera
shots; a "relief" view strips the imagery back to fog-shaded landform.

### [Ultra-Trail du Mont-Blanc](https://ebc-flythrough.pages.dev/utmb/)
The official 177 km race course around the Mont Blanc massif through France,
Italy and Switzerland, with roughly 10,000 m of ascent. All 31 official
checkpoints with their real cutoff times live in the HUD; a procedural chase
camera banks through the switchbacks.

### [New York City Marathon](https://ebc-flythrough.pages.dev/nyc/)
All 42.195 km across the five boroughs, with the city as a white architectural
massing model of 160,721 real buildings (heights from OpenStreetMap and NYC
Open Data) and the course lifted onto its five bridges. The camera flies the
street centreline and never clips a building over the full flight.

## How it works

No backend, no video. Real 3D, streamed:

1. A Python pipeline pulls elevation (Copernicus DEM, USGS 3DEP), satellite
   imagery (Sentinel-2), buildings (OSM + NYC Open Data) and the official
   course line, then bakes them into compressed mesh tiles (meshopt/glTF).
2. A React + Three.js app streams those tiles behind the scroll and scrubs a
   choreographed camera along the route — authored shot-by-shot for EBC,
   procedural for UTMB and NYC.
3. Everything ships as a static site: the whole app is ~430 KB gzipped, with
   10-31 MB of terrain per course streamed progressively. 60 fps on desktop and
   on the iPhone I have tested, targeting 30+ on mid-range mobile; Lighthouse
   100 for accessibility, including a full reduced-motion, keyboard-navigable
   chapter mode.

Each new course is a config + data drop, not a rebuild — the three above share
one codebase and one pipeline.

## Data & attribution

Copernicus DEM © ESA/Airbus · contains modified Copernicus Sentinel-2 data
2025 · elevation (NYC) USGS 3DEP · buildings and streets © OpenStreetMap
contributors (ODbL) · building heights via NYC Open Data (DOITT) · course routes
as published by UTMB Group and by NYRR.

Each course page carries the same attribution in its own colophon. The courses
are the official ones; this project is independent and is not affiliated with,
endorsed by, or commissioned by UTMB Group, NYRR or any race organiser.

## Source & contact

The source is private; this repository is the project's public face, and the
code is available for review on request.

Want a flythrough of your route — a trek, a race, a destination?
**[codingrajan@gmail.com](mailto:codingrajan@gmail.com)** ·
[LinkedIn](https://www.linkedin.com/in/rajanagarwal71/)

## Licence

The documentation in this repository is licensed
[CC BY 4.0](LICENSE) — quote it, cite it, build on it, with attribution.

That covers this repository's text only. The application and pipeline source
are private and are not licensed for reuse, and the datasets above carry their
own terms, which nothing here overrides.
