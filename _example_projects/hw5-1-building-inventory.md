---
name: Illinois Building Inventory Analysis - HW5.1
tools: [Python, Altair, Vega-Lite]
image: assets/pngs/buildings.png
description: Interactive visualizations exploring Illinois government building acquisitions and characteristics using the state building inventory dataset.
custom_js:
  - vega.min
  - vega-lite.min
  - vega-embed.min
  - justcharts
---

# Illinois Government Building Inventory Analysis

This analysis explores the Illinois government building inventory dataset, examining temporal patterns in building acquisitions and the relationship between building age and size across different state agencies.

## Visualization 1: Building Acquisitions Over Time by Agency

This interactive time series visualization displays the temporal patterns of building acquisitions by the top 5 Illinois government agencies from 1960 to 2015. The line chart uses quantitative encoding for both the year acquired (x-axis) and count of buildings (y-axis), with nominal color encoding to distinguish between different agencies using the category10 color scheme.

**Design Choices:** I selected a line chart with point markers to effectively communicate trends over time while preserving the ability to identify individual data points. The color scheme employs distinct hues for each agency: Department of Natural Resources (green), Historic Preservation Agency (blue), Department of Military Affairs (orange), Department of Agriculture (red), and Department of Juvenile Justice (purple). This categorical color encoding leverages pre-attentive processing, enabling viewers to quickly distinguish between agencies without conscious effort.

**Data Transformations:** The raw dataset underwent several preprocessing steps. First, I converted year fields to numeric type using pandas' to_numeric function with error coercion to handle non-numeric entries. Second, I aggregated the data by year and agency name using groupby operations, counting buildings acquired in each year. Finally, I filtered to include only the top 5 agencies by total building count to prevent visual clutter and focus analytical attention on the most significant institutional patterns.

**Interactivity:** The visualization implements interval selection (brush selection) bound to the x-axis encoding. Users can click and drag across the time axis to select a specific temporal range, which highlights the selected period at full opacity while dimming unselected periods to 20% opacity. This interaction pattern supports focused temporal analysis, allowing users to isolate and compare agency acquisition patterns during specific historical periods, such as during economic expansions or policy changes.

<vegachart schema-url="{{ site.baseurl }}/assets/json/hw5_chart1.json" style="width: 100%"></vegachart>

## Visualization 2: Building Size vs Age Relationship Across Agencies

This scatter plot explores the bivariate relationship between building age (years since construction) and square footage across different government agencies. The visualization uses quantitative encoding for both building age (x-axis) and square footage (y-axis with logarithmic scaling), combined with nominal color encoding for agencies using the tableau20 color scheme to accommodate the diversity of agencies in the dataset.

**Design Choices:** I chose a scatter plot because it effectively reveals correlations, clusters, and outliers in bivariate quantitative data. The logarithmic scale on the y-axis was essential given the extreme variation in building sizes, ranging from small facilities under 1,000 square feet to large government complexes exceeding 100,000 square feet. Without log scaling, smaller buildings would be compressed into an unreadable band at the bottom of the chart. Circle marks with 60% opacity help visualize density patterns where multiple buildings overlap, using transparency as a visual variable to encode point density.

**Data Transformations:** Multiple filtering steps ensured visual clarity and analytical validity. First, I removed extreme outliers by excluding buildings older than 150 years (likely data quality issues) and those larger than 500,000 square feet (extreme outliers that would compress the main distribution). Second, I calculated building age as 2024 minus year constructed. Third, for computational performance, I applied stratified random sampling when the filtered dataset exceeded 1,000 buildings, using a fixed random state (42) for reproducibility while maintaining representativeness across agencies.

**Interactivity:** The visualization features legend-based multi-selection interaction, where users can click agency names in the legend to selectively highlight or filter specific agencies. Selected agencies appear at 80% opacity with full color saturation, while unselected agencies fade to light gray at 10% opacity. This selection mechanism leverages the Gestalt principle of figure-ground segregation, enabling focused comparison of building characteristics across different government departments. For example, users can select the Department of Natural Resources and Department of Military Affairs simultaneously to compare their facility size and age distributions.

<vegachart schema-url="{{ site.baseurl }}/assets/json/hw5_chart2.json" style="width: 100%"></vegachart>

## Data Sources & Analysis Code

The analysis uses the Illinois government building inventory dataset, which contains detailed information about state-owned facilities including acquisition dates, construction years, square footage, and managing agencies.

<div class="left">
{% include elements/button.html link="https://raw.githubusercontent.com/UIUC-iSchool-DataViz/is445_data/main/building_inventory.csv" text="The Data" %}
</div>

<div class="right">
{% include elements/button.html link="https://colab.research.google.com/drive/1zgDLf-rdB9fl6kV6JkbYr_t1vartXfbJ" text="The Analysis" %}
</div>      
