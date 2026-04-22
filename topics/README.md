# Topic YAML

This folder contains the Copilot Studio code-editor import YAML for the two chart topics described in the guide.

Files:
- PrepareChartData.topic.yaml
- RenderChart.topic.yaml

These files now use the real AdaptiveDialog import structure:
- kind: AdaptiveDialog
- beginDialog / OnRecognizedIntent
- inputType / outputType
- SetVariable, ConditionGroup, BeginDialog, SendActivity, and SendMessage actions

Use them by creating a blank topic in Copilot Studio, opening the code editor, and pasting the file contents.
