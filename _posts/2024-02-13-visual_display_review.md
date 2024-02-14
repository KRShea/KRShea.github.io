---
title: Tuftian Box Plot and Book Review

published: false
date: 2024-02-13
tags: [Test]
---
### Big Title

Your introduction text here.

<div id="vega-vis"></div>

<script src="https://cdn.jsdelivr.net/npm/vega@5/build/vega.min.js"></script>
<script src="https://cdn.jsdelivr.net/npm/vega-lite@5/build/vega-lite.min.js"></script>
<script src="https://cdn.jsdelivr.net/npm/vega-embed@6/build/vega-embed.min.js"></script>

<script type="text/javascript">
  var spec = {
  "$schema": "https://vega.github.io/schema/vega/v5.json",
  "description": "Tuftian Box Plot",
  "author": "Kristopher Shea",
  "width": 200,
  "height": 200,
  "padding": 5,
  "background": "#ffffff",
   "signals": [
    {"name": "metric_column", "value": "Miles_per_Gallon"},
    {"name": "group_column", "value": "Cylinders"}
  ],
"title": {"text": {"signal": "metric_column + ' ~ ' + group_column"}, "offset": 20},
  "data": [
    {
      "name": "dataset",
      "url": "https://vega.github.io/vega/data/cars.json",
      "format": {"type": "json"}
    },
    {
      "name": "stats",
      "source": "dataset",
      "transform": [
        {
          "type": "aggregate",
          "groupby": [{"signal": "group_column"}],
          "fields": [
            {"signal": "metric_column"},
            {"signal": "metric_column"},
            {"signal": "metric_column"},
            {"signal": "metric_column"},
            {"signal": "metric_column"}
          ],
          "ops": ["q1", "q3", "median", "min", "max"],
          "as": ["q1", "q3", "median", "min", "max"]
        }
      ]
    }
  ],
  "scales": [
    {
      "name": "xscale",
      "type": "band",
      "domain": {"data": "stats", "field": "Cylinders", "sort": true},
      "range": "width",
      "padding": 0.2
    },
    {
      "name": "yscale",
      "type": "linear",
      "domain": {"data": "stats", "fields": ["min", "max"]},
      "range": "height",
      "nice": true,
      "zero": false
    }
  ],
  "axes": [
    {
      "orient": "bottom",
      "scale": "xscale",
      "domain": false,
      "title": {"signal": "group_column"},
      "titlePadding": 10
    },
    {
      "orient": "left",
      "scale": "yscale",
      "domain": false,
      "tickCount": 5,
      "title": {"signal": "metric_column"},
      "titlePadding": 10
    }
  ],
  "marks": [
    {
      "type": "symbol",
      "from": {"data": "stats"},
      "encode": {
        "enter": {
          "x": {
            "scale": "xscale",
            "field": {"signal": "group_column"},
            "band": 0.5
          },
          "y": {"scale": "yscale", "field": "median"},
          "fill": {"value": "black"},
          "size": {"value": 10},
          "tooltip": {
        "signal": "{'max': datum.max, 'q3': datum.q3, 'median': datum.median, 'q1': datum.q1, 'min': datum.min}"
      }
        }
      }
    },
    {
      "type": "rule",
      "from": {"data": "stats"},
      "encode": {
        "enter": {
          "x": {
            "scale": "xscale",
            "field": {"signal": "group_column"},
            "band": 0.5
          },
          "y": {"scale": "yscale", "field": "min"},
          "y2": {"scale": "yscale", "field": "q1"},
          "stroke": {"value": "black"},
          "strokeWidth": {"value": 1.25}
        }
      }
    },
    {
      "type": "rule",
      "from": {"data": "stats"},
      "encode": {
        "enter": {
          "x": {
            "scale": "xscale",
            "field": {"signal": "group_column"},
            "band": 0.5
          },
          "y": {"scale": "yscale", "field": "q3"},
          "y2": {"scale": "yscale", "field": "max"},
          "stroke": {"value": "black"},
          "strokeWidth": {"value": 1.25}
        }
      }
    }
  ]
}
;
  vegaEmbed('#vega-vis', spec);
</script>


### Other Big Title

## Hello

Test 123

Test 321