---
# You can also start simply with 'default'
theme: seriph
# random image from a curated Unsplash collection by Anthony
# like them? see https://unsplash.com/collections/94734566/slidev
background: https://cover.sli.dev
# some information about your slides (markdown enabled)
title: Presentation course
info: Presentation for the course
# apply unocss classes to the current slide
class: text-center
# https://sli.dev/features/drawing
drawings:
  persist: false
# slide transition: https://sli.dev/guide/animations.html#slide-transitions
transition: slide-left
# enable MDC Syntax: https://sli.dev/features/mdc
mdc: true
# open graph
seoMeta:
  # By default, Slidev will use ./og-image.png if it exists,
  # or generate one from the first slide if not found.
  ogImage: auto
  # ogImage: https://cover.sli.dev
  
hideInToc: true
---

# Cross Discipline Communication

---
hideInToc: true

---

# Contents
<Toc text-sm minDepth="1" maxDepth="1" />

---
layout: image-right
image: /images/footprint.png
---
# Context  

- How can we communicate with others about this piece of land?  
- We need all our users to be able to use the data 
  - Urban Planners  
  - Architects  
  - Software Engineers
---

# A first attempt

### How do we communicate about the site geometry?

````md magic-move {lines: true}

```json
{
  "site": <geometry>,
  "gpr": 3.0,
}
```


```json
// <well known text>
{
  "site": "POLYGON(...)",
  "gpr": 3.0,
}

// well known text is a common geospatial data interchange format
```

```json
// <well known binary>
{
  "site": 0xFFFFFF...,
  "gpr": 3.0,
}

// well known binary is the binary compressed version of well known text
// most dense format, but not human-readable
```

```json
// GeoJSON
{
  "site": {
    "type": "FeatureCollection",
    "features": [
      {
        "type": "Feature",
        "geometry": {
          "coordinates": [...],
        },
      }
    ]
  },
  "gpr": 3.0,
}

// geojson is a standard geospatial data interchange format
```

```json
// ESRI JSON
{
  "site": {
    "geometry": {
      "rings": [
        [
          ...
        ]
      ],
      "spatialReference": {
        "wkid": 4326
      }
    }
  },
  "gpr": 3.0,
}

// ESRI's flavour of geojson for serializing their data formats
// directly supported by ESRI's products
```

```json
// <well known text>
{
  "site": "POLYGON(...)",
  "gpr": 3.0,
}

// For simplicity, let's use WKT
```
````
---

# Variable Names  

<div v-click>

- Syntax  
  - How the information is structured
</div>
<div v-click>

- Semantics
  - What does the information represent to each group
  - urban planners, architects and software engineers have varying vocabularies
</div>

````md magic-move {lines: true}
```json
{
  "site": "POLYGON(...)",
  "gfa": 3.0,
}
```
```json
{
  "site": "POLYGON(...)",
  "gfa": 3.0,
}
// what aspect of the site is being described?
// what is gfa?
```
```json
{
  "site_boundary": "POLYGON(...)",
  "target_gross_plot_ratio": 3.0,
  // I can now research "gross plot ratio" for more information
}
```
````

---
layout: two-cols-header
---
# Coordinate systems

::left::

## 3d Graphics
<div v-click>

- X, Y, Z -> east, -elevation, north

</div>
<div v-click>

- Plane
  - Euclidean (flat ground)
<br>
<br>
</div>
<div v-click>

![](/images/coord_right.jpg)

</div>

::right::

## Cartographic
<div v-click>

- X, Y, Z -> east, north, elevation
</div>
<div v-click>

- Plane 
  - 🌏 WGS84 (projected on ellipsoid)
  - 🗺️ SVY21 (projected on flat ground)

</div>
<div v-click>

![](/images/coord_left.jpg)

</div>


---
layout: quote

---

# Look how far we've come 

````md magic-move {lines: true}
```json
{
  "site": <geometry>,
  "gpr": 3.0,
}
```
```json
{
  "site_boundary": "POLYGON(...)",
  "coordinate_system": "EPSG:3414", // EPSG:3414 is the code for svy21
  "target_gross_plot_ratio": 3.0,
}
```
```json
// and this is just for a small example
{
  "site_boundary": "POLYGON(...)",
  "coordinate_system": "EPSG:3414", // EPSG:3414 is the code for svy21
  "target_gross_plot_ratio": 3.0,
}
```
````
<div v-click>
<img src="/images/eplanner.png" style="width: 55%"/>
</div>
