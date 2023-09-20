
# Dynamic Chart with Real-Time Data

This is a simple web application that demonstrates how to create a dynamic chart with real-time data using [Chart.js](https://www.chartjs.org/). The chart updates automatically to display changing data.

## Prerequisites

Before you start, make sure you have the following:

- A modern web browser
- Internet access to load Chart.js library from CDN


## Usage

To use this code in your project, follow these steps:

1. Include the Chart.js library in your HTML file. You can add the following line to your `<head>` section:

   ```html
   <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
   ```

2. Create an HTML canvas element where you want to display the chart. For example:

   ```html
   <div style="width: 80%; margin: auto;">
       <canvas id="realTimeChart"></canvas>
   </div>
   ```

3. Include the CSS and JavaScript files:

   ```html
   <link rel="stylesheet" href="style.css">
   <script src="script.js"></script>
   ```

4. Initialize and configure your dynamic chart in your JavaScript code. You can modify the `script.js` file in this repository as a reference.
Certainly! Let me explain the JavaScript code included in the `script.js` file:

```javascript
const ctx = document.getElementById('realTimeChart').getContext('2d');
```
- This line selects the HTML `<canvas>` element with the `id` of `realTimeChart` and gets its 2D rendering context (`getContext('2d')`). This context is used to draw the chart on the canvas.

```javascript
let chart;
```
- Declares a variable `chart` which will store the Chart.js chart instance.

```javascript
const initialData = {
    labels: [],
    datasets: [{
        label: 'Value',
        data: [],
        borderColor: 'rgba(75, 192, 192, 1)',
        borderWidth: 1,
        fill: false,
    }],
};
```
- `initialData` is an object that defines the initial data for the chart. It includes:
  - `labels`: An empty array to store the x-axis labels.
  - `datasets`: An array containing an object representing the dataset. This dataset has a label, empty data array, and styling properties for the chart line.

```javascript
const chartConfig = {
    type: 'line',
    data: initialData,
    options: {
        scales: {
            x: {
                type: 'linear',
                position: 'bottom',
                title: {
                    display: true,
                    text: 'Time',
                },
            },
            y: {
                beginAtZero: true,
                title: {
                    display: true,
                    text: 'Value',
                },
            },
        },
        animation: false,
    },
};
```
- `chartConfig` is an object that configures the chart's type (line chart), initial data (`initialData`), and various chart options.
- The `scales` section defines the x and y axes configurations, including axis titles.
- `animation` is set to `false` to disable chart animations.

```javascript
chart = new Chart(ctx, chartConfig);
```
- This line creates a new Chart.js chart instance using the canvas context (`ctx`) and the configuration object (`chartConfig`).

```javascript
function addData() {
    const newData = Math.random() * 1000;
    chart.data.labels.push(chart.data.labels.length);
    chart.data.datasets[0].data.push(newData);
    chart.update();
}
```
- `addData` is a function that adds new data points to the chart at regular intervals.
- It generates a random number (`newData`) between 0 and 1000.
- It pushes a new label (incremented length of the labels array) and the `newData` value to their respective arrays in the chart's data.
- Finally, it updates the chart to reflect the changes using `chart.update()`.

```javascript
setInterval(addData, 1000);
```
- This sets up an interval that calls the `addData` function every 1000 milliseconds (1 second). This simulates real-time data updates and causes the chart to continuously add new data points.