# Chart Test Prompts

Use these as full prompts in chat. Each one tells the agent what to render and includes the data inline.

If the bot responds with a text summary instead of a visual chart, use the strict prompts in the section near the bottom of this file.

## Horizontal bar

```text
Render a horizontal bar chart for open tickets by team. Use this data: Support 42, Sales 18, Finance 11, and HR 7. Title it Open Tickets by Team, use Team for the x-axis, Tickets for the y-axis, and use a categorical color set.
```

## Pie

```text
Render a pie chart showing market share. Use this data: Product A 45, Product B 30, Product C 15, and Other 10. Title it Market Share and use a categorical color set.
```

## Line

Note: line charts render best when the x-axis uses ordered numeric or date-like values. For month names such as Jan, Feb, and Mar, a grouped bar chart may look better unless you pass actual dates.

```text
Render a line chart titled Monthly Revenue Trend. Use Date for the x-axis and Revenue for the y-axis. Plot one series called Revenue with these values: 2026-01-01 = 120, 2026-02-01 = 135, 2026-03-01 = 128, 2026-04-01 = 150, and 2026-05-01 = 165. Use a categorical color set.
```

## Vertical bar grouped

```text
Render a grouped vertical bar chart titled Quarterly Sales by Region. Use Quarter for the x-axis and Sales for the y-axis. Include two series: East with Q1 55, Q2 68, Q3 72, Q4 80; and West with Q1 48, Q2 60, Q3 66, Q4 74. Use a categorical color set.
```

## Horizontal bar stacked

```text
Render a stacked horizontal bar chart titled Project Effort by Team. Include Website Redesign with Design 25 in good, Build 45 in warning, and QA 30 in attention. Include Mobile App with Design 20 in good, Build 50 in warning, and QA 30 in attention.
```

## Strict chart-only prompts

Use these when the bot keeps summarizing the data in plain text. These explicitly ask it to call the chart topic and return only the card.

```text
Use the Render Chart topic and return only the chart card with no prose summary. Render this line chart using the following chart plan JSON: {"chartType":"line","title":"Monthly Revenue Trend","xAxisTitle":"Date","yAxisTitle":"Revenue","colorSet":"categorical","data":[{"legend":"Revenue","values":[{"x":"2026-01-01","y":120},{"x":"2026-02-01","y":135},{"x":"2026-03-01","y":128},{"x":"2026-04-01","y":150},{"x":"2026-05-01","y":165}]}]}
```

```text
Use the Render Chart topic and return only the chart card with no prose summary. Render this stacked horizontal bar chart using the following chart plan JSON: {"chartType":"horizontalbarstacked","title":"Project Effort by Team","stackedBarData":[{"title":"Website Redesign","data":[{"legend":"Design","value":25,"color":"good"},{"legend":"Build","value":45,"color":"warning"},{"legend":"QA","value":30,"color":"attention"}]},{"title":"Mobile App","data":[{"legend":"Design","value":20,"color":"good"},{"legend":"Build","value":50,"color":"warning"},{"legend":"QA","value":30,"color":"attention"}]}]}
```

## JSON-backed prompts

If your orchestration works better with explicit chart plans, you can also send prompts like these:

```text
Render a chart using this chart plan JSON: {"chartType":"horizontalbar","title":"Open Tickets by Team","xAxisTitle":"Team","yAxisTitle":"Tickets","colorSet":"categorical","normalizedRows":[{"category":"Support","value":42},{"category":"Sales","value":18},{"category":"Finance","value":11},{"category":"HR","value":7}]}
```

```text
Render a chart using this chart plan JSON: {"chartType":"pie","title":"Market Share","colorSet":"categorical","normalizedRows":[{"category":"Product A","value":45},{"category":"Product B","value":30},{"category":"Product C","value":15},{"category":"Other","value":10}]}
```

```text
Render a chart using this chart plan JSON: {"chartType":"line","title":"Monthly Revenue Trend","xAxisTitle":"Date","yAxisTitle":"Revenue","colorSet":"categorical","data":[{"legend":"Revenue","values":[{"x":"2026-01-01","y":120},{"x":"2026-02-01","y":135},{"x":"2026-03-01","y":128},{"x":"2026-04-01","y":150},{"x":"2026-05-01","y":165}]}]}
```

