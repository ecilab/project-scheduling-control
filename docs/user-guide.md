# User guide

This guide walks through the Project Scheduling & Critical Path Analyzer from entering activities to reading the results.

## 1. The header

- **Project name:** type a name for your project. The chevron at the right of the box opens the list of example projects.
- **Project completion time:** the total project duration, updated as you type. The mini Gantt chart on the card shows the critical path, with a flag at the finish.

The control bar below the header holds: New Project, the example picker and Load Example, Save, Reset Project (back to the last save), Import, Export, the language switch (English / العربية) and the light/dark theme.

## 2. Entering activities

Each row in the **Activities** table has four fields:

| Field | Rules |
|---|---|
| Activity No. | Letters, digits, `_` or `.`; must be unique (e.g. `1`, `A`, `2.1`) |
| Activity Name | Required |
| Duration | A number ≥ 0. Zero is allowed and is treated as a milestone. Decimals are allowed. |
| Predecessor | Activity numbers separated by commas (`4,5`). Leave empty or type `-` for a starting activity. |

- **Enter** moves to the next row; Enter on the last row adds a new activity.
- The **Status** column shows whether each activity is critical or how much float it has.
- Errors are listed above the table and the faulty cells are outlined in red. The schedule is not calculated until every error is fixed. Warnings (for example a zero duration) do not block the calculation.

### Loading an example
Click one of the example cards above the table. The card of the loaded example is tagged **Loaded**.

### Importing a CSV file
Use `examples/template.csv` as a starting point. The file must have the columns *Activity No., Activity Name, Duration, Predecessor*. Put multiple predecessors in quotes: `"2,3"`.

## 3. KPI cards

Six cards summarise the schedule: total activities, project duration, critical activities, critical path, total float and maximum float. Each illustration is drawn from your project. Clicking a card takes you to the related view (for example, *Critical Path* traces the path on the network diagram).

## 4. Gantt chart

- Each bar runs from the activity's earliest start (ES) to its earliest finish (EF).
- **Red** bars are critical, **blue** bars have float, and **purple/teal** bars have large float (at least 25% of the project duration).
- The **dashed tail** after a bar shows its total float, up to the latest finish (LF).
- Hover over a bar to see its values and highlight its predecessors and successors. Click it to open the details panel.
- **Highlight Critical Path** dims the other activities and traces each critical path step by step. **Reset View** clears it.
- **Play Schedule** moves a time cursor from 0 to the finish; completed activities turn green.
- **Time unit** changes the axis label only (minutes, hours, days, weeks, months or time units).
- **Zoom:** Fit Project, zoom in and zoom out. Long projects scroll horizontally.

## 5. Critical path summary

Every critical path is listed with its activities and the sum of their durations, which always equals the project completion time.

## 6. Network diagram

Activity-on-node diagram. Each node shows ES, EF, LS, LF and total float; critical nodes and links are red. **Animate Critical Path** runs a marker along the critical links. **Fit to width** shrinks large networks to the screen.

## 7. CPM analysis table

All calculated values for every activity, including free float. Critical rows are highlighted. Click a row for details.

## 8. Schedule analysis

Statements generated from the calculated schedule (duration, critical path, float, merge points, longest activity) and four indicators: schedule risk, criticality ratio, schedule flexibility and the potential bottleneck. The risk rule is shown on screen. These are deterministic scheduling indicators, not statistical predictions.

## 9. Saving, exporting and printing

- The project is saved automatically in your browser. **Save** stores a copy that **Reset Project** can return to.
- **Export:** Gantt chart as PNG, CPM table as CSV, activities as CSV, project as JSON.
- **Print report** produces a landscape report with the summary, Gantt chart, critical path, network, CPM table and analysis.
