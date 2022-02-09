---
title: "Interpolation"
slug: "interpolation"
description: "How interpolation between measurement values works."
---

* toc
{:toc}

# Setup
```javascript
// Example data
// (most recent soil height measurement for each 10mm-rounded location where data exists)
var points = [
  { uuid: "A", body: { x: 0, y: 0, z: 0 } },
  { uuid: "B", body: { x: 10, y: 10, z: 10 } },
];

// Example position
var position = { x: 4, y: 4 };

// Library
var script = document.createElement('script');
script.type = 'text/javascript';
script.src = 'https://cdn.jsdelivr.net/npm/lodash@4/lodash.min.js';
document.head.appendChild(script);
```

# Nearest Neighbor
```javascript
var distance = (from, to) =>
  Math.pow(Math.pow(to.x - from.x, 2) + Math.pow(to.y - from.y, 2), 0.5);
var nearest = _.sortBy(points.map(p =>
 ({ point: p, distance: distance(position, p.body) })), "distance")[0];
var z = nearest.point.body.z;

// expected z using example data: 0
```

# Inverse Distance Weighting
```javascript
var distance = (from, to) =>
  Math.pow(Math.pow(to.x - from.x, 2) + Math.pow(to.y - from.y, 2), 0.5);
var nearest = _.sortBy(points.map(p =>
 ({ point: p, distance: distance(position, p.body) })), "distance")[0];
var z = nearest.distance == 0
  ? nearest.point.body.z
  : _.sum(points.map(p => (1 / distance(position, p.body) ** 4) * p.body.z))
  / _.sum(points.map(p => (1 / distance(position, p.body) ** 4)));

// expected z using example data: 1.65
```
