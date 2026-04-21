# Copilot Studio Adaptive Cards

This repository shows a reusable pattern for rendering Adaptive Card charts from JSON data in Copilot Studio.

The included guide uses a music dataset as the example scenario, but the pattern is intended to work for many kinds of structured data.

## Contents

- [CopilotStudio-AdaptiveCharts-Guide.md](CopilotStudio-AdaptiveCharts-Guide.md) - step-by-step guide for the topic pattern
- [Reference/](Reference/) - sample chart payloads and supporting reference material

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
