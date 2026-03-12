# GristSub Widget Documentation

## Overview
This documentation provides an overview of the **GristSub** project widgets: **gristsub.html** and **Sub_dash**.

## gristsub.html Widget
### Purpose
The **gristsub.html** widget is designed to facilitate seamless data interactions and visualizations. It integrates with data sources and renders them in an engaging manner.

### Features
- Interactive UI for data manipulation.
- Supports various data formats for input.
- Allows real-time data updates and visualizations.

### Usage
To use the **gristsub.html** widget:
1. Include the widget in your HTML as follows:
   ```html
   <script src="path/to/gristsub.html"></script>
   ```
2. Initialize the widget with your desired configurations:
   ```javascript
   const gristSub = new GristSubWidget({
       dataSource: 'your-data-source',
       options: { ... }
   });
   ```

## Sub_dash Widget
### Purpose
The **Sub_dash** widget serves as a dashboard interface that consolidates metrics and insights from various data sources into one unified view.

### Features
- Customizable dashboard layouts.
- Drag-and-drop functionality for arranging components.
- Responsive design for mobile and desktop.

### Usage
To integrate the **Sub_dash** widget into your project:
1. Add the following script to your HTML file:
   ```html
   <script src="path/to/Sub_dash.js"></script>
   ```
2. Configure the dashboard with your desired metrics:
   ```javascript
   const subDash = new SubDashWidget({
       metrics: ['metric1', 'metric2'],
       layout: 'grid',
   });
   ```

## Conclusion
With both **gristsub.html** and **Sub_dash**, you can create rich data-driven applications that enhance user engagement and provide insightful analytics.