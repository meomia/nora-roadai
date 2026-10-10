# Reducing Emissions in Road Construction Rubble Transport

Entry to the **RoadAI – Reducing emissions in road construction** competition, hosted by the Norwegian Artificial Intelligence Research Consortium (NORA) with Skanska Norge. Published as:

> Shturmov O. & Moskalova D. *Reducing Emissions in Road Construction Rubble Transport.* Nordic Machine Intelligence, vol. 10, pp. 11–14, 2023. ([paper.pdf](paper.pdf))

## Problem

Roughly 1.5% of Norway's greenhouse gas emissions come from construction machines, much of it from trucks hauling rubble across mountainous terrain. Using GPS and trip data from Skanska's dumpers and trucks, we looked at how to (a) schedule trucks so they arrive at a loading site only when needed and leave fully loaded, and (b) choose an efficient driving scheme between loading and dump sites.

## Approach

- **Data exploration** – trip patterns per machine type, haversine trip distances, geohash encoding to find frequently visited locations.
- **Automatic site detection** – the provided load/dump coordinates rely on manual input, so we derived them from GPS data:
  - **Loading sites** as convex hulls of dumper positions per material (where dumpers and trucks intersect).
  - **Dump sites** via **DBSCAN** density clustering of truck GPS points, distinguishing load vs. dump by timestamps and hull intersection.
- **Rubble generation model** – a linear model of how fast material is produced at a loading site, from historical truck entry/exit times and carried mass, as the basis for a truck arrival schedule.
- **Elevation** – factoring in elevation data to inform the driving scheme between sites.

## Files

- `Discovering_the_data.ipynb` – first exploration, geohashing, DBSCAN experiments, elevation lookups
- `Exploring loading sites.ipynb` – loading-site detection with convex hulls and DBSCAN
- `Trip patterns.ipynb` – dumper vs. truck movement, load generation per minute, arrival schedule
- `GPSData/` – competition sample data (trips and trip info, March 2022)
- `paper.pdf` – published paper (CC BY 4.0)

**Stack:** Python · pandas · GeoPandas · Shapely · scikit-learn (DBSCAN) · Folium · Matplotlib · seaborn
