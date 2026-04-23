# Copilot Studio Adaptive Cards

This repository shows a reusable pattern for rendering Adaptive Card charts from JSON data in Copilot Studio.

The included guide uses a music dataset as the example scenario, but the pattern is intended to work for many kinds of structured data.

## Contents

- [CopilotStudio-AdaptiveCharts-Guide.md](CopilotStudio-AdaptiveCharts-Guide.md) - step-by-step guide for the topic pattern
- [topics/PrepareChartData.topic.yaml](topics/PrepareChartData.topic.yaml) - Copilot Studio YAML for the data-normalization topic
- [topics/RenderChart.topic.yaml](topics/RenderChart.topic.yaml) - Copilot Studio YAML for the chart-rendering topic

## Goal

The goal of this repo is to demonstrate how to:

1. accept structured JSON from an orchestrator or agent
2. normalize the data into a chart-friendly contract
3. render Adaptive Card charts in Copilot Studio

## Pattern

The guide demonstrates a two-topic pattern:

- Prepare Chart Data
- Render Chart

This separation of concerns keeps data shaping separate from presentation and makes the approach easier to reuse.

## Topic YAML

The [topics](topics) folder contains the Copilot Studio code-editor import YAML for the two chart topics described in the guide.

Included files:

- [topics/PrepareChartData.topic.yaml](topics/PrepareChartData.topic.yaml)
- [topics/RenderChart.topic.yaml](topics/RenderChart.topic.yaml)

These files follow the AdaptiveDialog code-editor structure used by Copilot Studio, including:

- `kind: AdaptiveDialog`
- `beginDialog` or `OnRecognizedIntent`
- `inputType` and `outputType`
- `SetVariable`, `ConditionGroup`, `BeginDialog`, `SendActivity`, and `SendMessage` actions

Use them by creating a blank topic in Copilot Studio, opening the code editor, and pasting the file contents.

If cross-topic references do not bind cleanly after paste, reselect the target topic in the Copilot Studio canvas instead of assuming the imported redirect reference will remain valid across environments.

## Additive Chart Instructions

Use this only as an add-on to existing agent instructions. It covers the minimum behavior needed to hand off chart requests to the two chart topics in this repo.

```text
When the user asks for a chart and the returned data can be normalized, call Prepare Chart Data first and then Render Chart. Do not call Render Chart directly from a raw user request unless you already have a fully normalized ChartPlanJSON object.

Pass SelectedDatasetJSON as valid JSON.

Never pass prose, markdown tables, or raw Adaptive Card JSON into chart topic inputs.

Normalize the dataset before topic handoff:
- category: main label or bucket
- value: numeric measure
- series: optional grouping dimension

Clean numeric strings so values like 1,508 become numbers.

Choose chart types with these rules:
- pie: one label field and one numeric field with a small number of categories
- horizontalBar: rankings, top-N, and simple comparisons
- line: time-based trends with ordered x values
- verticalBarGrouped: multi-series comparisons
- verticalBarStacked: totals plus composition across categories
- horizontalBarStacked: composition within each category

If a line chart uses month labels such as Jan, Feb, and Mar, normalize them to ISO-like dates such as 2026-01-01, 2026-02-01, and 2026-03-01 before building the chart plan. If the labels must remain unchanged, prefer a bar chart instead.

Build SelectedDatasetJSON in this shape whenever possible:

{
  "title": "...",
  "preferredChartType": "horizontalBar",
  "xAxisTitle": "...",
  "yAxisTitle": "...",
  "rows": [
    { "label": "...", "value": 123 }
  ]
}

Render Chart expects ChartPlanJSON in these shapes:
- horizontalBar or pie: normalizedRows with category and value
- line, verticalBarGrouped, verticalBarStacked: data as series objects with legend and values, where each point has x and y
- horizontalBarStacked: stackedBarData with a title per bar and a nested data array of legend, value, and color

If the data is too ambiguous to map safely, ask a clarifying question instead of sending a malformed chart payload.
```
