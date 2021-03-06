Scatter Plot Brush:

<div id="scatter-garbage" class="demo"></div>
<script src="/react-d3-example/dist/min/es5/scatter_garbage_brush.min.js"></script>

```js
"use strict"

var React = require('react');
var ScatterBrush = require('react-d3-brush').ScatterBrush;

(function() {
  // load your general data
  var chartData = require('dsv?delimiter=,!../data/garbage.csv');

  // your date format, use for parsing
  var parseDate = d3.time.format("%YM%m").parse;

  var width = 700,
    height = 300,
    margins = {top: 30, right: 70, bottom: 30, left: 50},
    id = "simple-area-chart",
    title = "Taiwan refuse disposal - Multi line",
    svgClassName = "simple-area-chart",
    titleClassName = "test-chart-title-class",
    // show legend or not
    showLegend = true,
    // show xaxis or not
    showXAxis = true,
    // show yaxis or not
    showYAxis = true,
    // chart series,
    // field: is what field your data want to be selected
    // name: the name of the field that display in legend
    // color: what color is the line
    chartSeries = [
      {
        field: 'total',
        name: 'Total',
        symbol: 'diamond',
        symbolSize: 6
      },
      {
        field: 'incineration',
        name: 'Incineration',
        symbol: 'cross',
        symbolSize: 6
      },
      {
        field: 'garbageBury',
        name: 'Garbage Bury',
        symbol: 'triangle-down',
        symbolSize: 6
      }
    ],
    // your x accessor
    x = function(d) {
      return parseDate(d.month);
    },
    xOrient = 'bottom',
    xTickOrient = 'bottom',
    xDomain = d3.extent(chartData, function(d){ return x(d) }),
    xRange = [0, width - margins.left - margins.right],
    xScale = 'time',
    xAxisClassName = 'x-axis',
    xLabel = "Month",
    xLabelPosition = "left",
    // your y accessor
    y = function(d) {
      return +d;
    },
    yOrient = 'right',
    yTickOrient = 'right',
    // find max and min
    yDomain = [0, d3.max(chartData, function(d) {return d.total;})],
    yRange = [height - margins.top - margins.bottom, 0],
    yScale = 'linear',
    yAxisClassName = 'y-axis',
    yLabelPosition = 'left',
    yLabel = "Amount",
    categoricalColors= d3.scale.category10(),
    // your brush height
    brushHeight = 100;

  React.render(
      <ScatterBrush
        title= {title}
        data= {chartData}
        width= {width}
        height= {height}
        id= {id}
        margins= {margins}
        svgClassName= {svgClassName}
        titleClassName= {titleClassName}
        yAxisClassName= {yAxisClassName}
        xAxisClassName= {xAxisClassName}
        chartSeries= {chartSeries}
        showLegend= {showLegend}
        showXAxis= {showXAxis}
        showYAxis= {showYAxis}
        x= {x}
        xDomain= {xDomain}
        xRange= {xRange}
        xScale= {xScale}
        xOrient= {xOrient}
        xTickOrient= {xTickOrient}
        xLabel = {xLabel}
        xLabelPosition = {xLabelPosition}
        y= {y}
        yOrient= {yOrient}
        yDomain= {yDomain}
        yRange= {yRange}
        yScale= {yScale}
        yTickOrient= {yTickOrient}
        yLabel = {yLabel}
        yLabelPosition = {yLabelPosition}
        categoricalColors= {d3.scale.category10()}
        brushHeight= {brushHeight}
      />
  , document.getElementById('scatter-garbage')
  )
})()
```
