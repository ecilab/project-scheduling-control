# User guide

This guide walks through Project Scheduling & Control from entering activities to reading the results.

## 1. The header

- **Project name:** type a name for your project. The chevron at the right of the box opens the list of example projects.
- **Project completion time:** the total project duration, updated as you type. The mini Gantt chart on the card shows the critical path, with a flag at the finish.

The control bar below the header holds: New Project, the example picker and Load Example, Save, Reset Project (back to the last save), Import, Export, **Practice** (see section 12) and the optional **AI assistant** (see section 13). The language switch (English / العربية) and the light/dark theme are in the upper corner of the header.

## 2. Entering activities

Each row in the **Activities** table has four fields:

| Field | Rules |
|---|---|
| Activity No. | Letters, digits, `_` or `.`; must be unique (e.g. `1`, `A`, `2.1`) |
| Activity Name | Required |
| Duration | A number ≥ 0. Zero is allowed and is treated as a milestone. Decimals are allowed. |
| Predecessor | Activity numbers separated by commas (`4,5`). Leave empty or type `-` for a starting activity. Relationship types and lags are written after the number (see below). |

- **Enter** moves to the next row; Enter on the last row adds a new activity.
- The **Status** column shows whether each activity is critical or how much float it has.
- Errors are listed above the table and the faulty cells are outlined in red. The schedule is not calculated until every error is fixed. Warnings (for example a zero duration) do not block the calculation.

### Relationship types and lags
A plain number is a finish-to-start link. Add a type and an optional lag (in the project's time unit) for the precedence diagramming method used by MS Project and Primavera:

| Entry | Meaning |
|---|---|
| `4` | Finish-to-start: this activity starts after 4 finishes |
| `4+2` or `4FS+2` | Finish-to-start with a 2-unit lag |
| `4FS-1` | Finish-to-start with a 1-unit lead (a negative lag needs the type) |
| `4SS+2` | Start-to-start: starts at least 2 units after 4 starts |
| `4FF` | Finish-to-finish: finishes no earlier than 4 finishes |
| `4SF` | Start-to-finish |

Only one relationship is allowed between the same two activities. The **Relationships with lags** example shows overlapping work.

### Extra columns
The chips above the table switch on optional column groups. They are saved and exported with the project.

| Group | Columns | Used by |
|---|---|---|
| PERT estimates | Optimistic *a*, most likely *m*, pessimistic *b* | PERT, Monte Carlo. When all three are filled, the Duration cell shows the expected time *te* (read-only). |
| Costs & crashing | Crash duration, normal cost, crash cost | Crashing, earned value (the normal cost is the budget), scenarios |
| Resources | Units required per time unit | Resources |
| Progress | % complete, actual cost | Earned value, progress shading on the Gantt chart |

### Loading an example
Click one of the example cards above the table. The card of the loaded example is tagged **Loaded**.

### Importing a CSV file
Use `examples/template.csv` as a starting point. The file must have the columns *Activity No., Activity Name, Duration, Predecessor*. Put multiple predecessors in quotes: `"2,3"`. Optional columns are recognised by their headers (*Optimistic, Most likely, Pessimistic, Crash duration, Normal cost, Crash cost, Resource units, % complete, Actual cost*) and switch on the matching column group.

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
- **Calendar** opens the project calendar: a start date, the weekend (Friday and Saturday, Saturday and Sunday, Friday only, Sunday only, or none) and holidays as `YYYY-MM-DD` dates. With a start date and the time unit set to Days, the axis, tooltips, CPM table, details panel and exports show real dates. Day *t* is the *t*-th working day, so an activity with ES = 3 and duration 2 works on working days 3 and 4.
- **Baseline** (shown once a baseline is saved on the Earned value tab) draws the baseline dates as thin grey bars under each activity. With the Progress columns on, the completed part of each bar is shaded.
- Links follow their relationship type: start-to-start arrows join the bar starts, finish-to-finish arrows join the bar ends.

## 5. Critical path summary

Every critical path is listed with its activities and the sum of their durations (plus any lags), which equals the project completion time. When a path uses start-to-start or finish-to-finish links the activities overlap, so the summary says so instead of adding the durations.

## 6. Network diagram

**AON** (the default) is the activity-on-node diagram. Each node shows ES, EF, LS, LF and total float; critical nodes and links are red, and links with a type or lag carry a label such as `SS+2`. **Animate Critical Path** runs a marker along the critical links. **Fit to width** shrinks large networks to the screen.

**AOA** draws the same project as an activity-on-arrow network. Activities are arrows labelled *number (duration)*; dashed arrows are dummy activities. Each event circle shows its number, the earliest event time (left) and the latest event time (right). The tool adds only the dummies needed to keep the dependencies correct and to stop two activities sharing the same pair of events. AOA cannot show lags or SS/FF/SF links, so it is not drawn for such projects.

## 7. CPM analysis table

All calculated values for every activity, including free float. Critical rows are highlighted. Click a row for details.

## 7a. Step-by-step solution

Every value is written out with its actual numbers, the way it is written on the board:

```
ES₇ = max(EF₄, EF₅) = max(12, 14) = 14
LF₂ = min(LS₄, LS₆) = min(8, 12) = 8
FF₂ = min(ES₄, ES₆) − EF₂ = min(6, 6) − 6 = 0
```

The steps follow the order of the method: forward pass in topological order, project duration, backward pass in reverse order, float, then the critical activities and paths. Where an activity has several predecessors or successors, a note explains why the largest or smallest value is taken. Lags and SS/FF/SF links appear in the formulas (for example `ES₄ = EF₃ + 1 − d₄ = 15 + 1 − 8 = 8`).

- **Play the solution** runs the steps one by one on a copy of the network. The cells fill in as each value is calculated, the activity being calculated is outlined in cyan and the activities it uses in amber. Use the arrows to step back and forward, ×1/×2/×4 for the speed, **Show all steps** to see the full solution, or click any line to jump to it.
- **Answer sheet** opens a printable model answer (save it as PDF from the print dialog): the given data, every step with its numbers, the network diagram, the summary table and the critical path. It is also in the Export menu.
- The details panel of each activity lists how its six values were calculated.

Students can check a hand solution line by line rather than only the final numbers. The panel is hidden in practice mode.

## 8. Schedule analysis

Statements generated from the calculated schedule (duration, critical path, float, merge points, longest activity) and four indicators: schedule risk, criticality ratio, schedule flexibility and the potential bottleneck. The risk rule is shown on screen. These are deterministic scheduling indicators, not statistical predictions.

## 9. Saving, exporting and printing

- The project is saved automatically in your browser. **Save** stores a copy that **Reset Project** can return to.
- **Export:** Gantt chart as PNG, CPM table as CSV, activities as CSV, project as JSON, **Excel workbook (.xlsx)** and **MS Project XML**.
  - The Excel workbook has an Activities sheet and a CPM sheet whose ES, EF, LS, LF, float and project duration are live Excel formulas, so changing a duration in Excel updates the schedule. PERT, crashing, resources, earned value and Monte Carlo sheets are added when that data exists.
  - The MS Project file (MSPDI) holds the tasks, the links with their type and lag, the calendar with weekends and holidays, costs, % complete and the resource. Open it in Microsoft Project with *File › Open* and choose the XML file type. ProjectLibre also reads it.
- The project JSON also stores the calendar, the baseline, the progress records and the scenarios.
- **Print report** produces a landscape report with the summary, Gantt chart, critical path, network, CPM table and analysis.

## 10. Advanced analysis

The tabs below the analysis section hold six tools. When data is missing, each tab explains what it needs and offers a button that switches on the right columns.

### PERT
Enter *a*, *m* and *b* for each activity. The tool computes *te* = (*a* + 4*m* + *b*) / 6 and σ² = ((*b* − *a*) / 6)² for every activity, runs CPM with the expected times and adds the variances along the critical path. With several critical paths it uses the one with the largest variance. Type a **target completion time** to get *z* = (target − T) / σ and P(T ≤ target) from the normal distribution; type a **required probability** to get the duration that achieves it. The working is shown step by step next to the chart. Activities without estimates keep a fixed duration (variance 0).

### Monte Carlo
Runs 1,000 to 50,000 schedules, each with every duration drawn from its *a*–*m*–*b* range (Beta-PERT or triangular). It shows the mean, P50, P80 and P90, the histogram and cumulative curve of the completion time, the chance of meeting the target, and the **criticality index** (how often each activity was critical) with the correlation between each activity's duration and the project duration. Enter a **seed** to repeat exactly the same runs, for example so that a whole class gets identical numbers. The comparison with the PERT formula shows the merge bias: where paths join, the expected finish is later than the sum of the expected times.

### Crashing
Enter crash durations, normal costs and crash costs, then the **indirect cost** per time unit. Starting from the normal schedule, each step shortens the project by up to one time unit at the lowest cost. With parallel critical paths every path must be shortened, so the tool chooses the cheapest combination of activities (a minimum cut of the critical network). A step is also stopped early when a non-critical path becomes critical. The table lists each step with its direct, indirect and total cost, the chart plots the three curves against duration, and the optimum (lowest total cost) is marked. **Scenario** on any row saves that crashed schedule for comparison.

### Resources
Enter the units each activity needs and, optionally, a resource name and the units available. Then choose a view:
- **Early start** and **Late start:** the resource histogram when every activity starts at its ES or its LS.
- **Levelled:** non-critical activities are moved within their float to make the histogram as flat as possible (minimum Σ r², the Burgess method). The project duration does not change.
- **Within limit** (when units available is set): activities are scheduled in order of least late start so that demand never exceeds the limit. The project may get longer.

Under the histogram, each activity bar is drawn in the chosen schedule over its float window, and shifted activities are coloured. The tables compare the peak, Σ r², time over the limit and duration of each view.

### Earned value
1. **Save baseline** freezes the current plan: the planned start, finish and budget of every activity. The budget is the normal cost, or the duration when no costs were entered.
2. As work progresses, enter **% complete** and **actual cost** in the activity table and set the **status date**.
3. The tab shows PV, EV, AC, SV, CV, SPI, CPI, EAC, ETC, VAC, TCPI and the earned schedule with its forecast duration, together with statements that interpret them.
4. **Record this status** stores the values at that date; the recorded points build the EV and AC S-curves against the planned value curve.

The Gantt chart shows the baseline as grey bars under the current schedule.

### Scenarios
Type a name and choose **Save current as scenario** to keep a what-if version (for example "Base case"). Change durations or links and save again. The table compares every scenario with the current project: duration, finish date, critical activities and path, total float, direct and total cost, PERT probability and resource peak. The best value in each row is marked and the activities that differ are listed. **Load** makes a scenario the current project (Undo is offered), **Update** overwrites it with the current project, and the name can be edited in place.

## 11. Example data for the advanced tools

Every example carries the data for all the tools, so each tab works as soon as an example is loaded:

| Data | In every example |
|---|---|
| PERT estimates | *a*, *m* and *b* for each activity, chosen so that *te* equals the original duration. The CPM answers in the exercises therefore do not change. |
| Costs and crashing | Normal cost, crash duration and crash cost (a few activities cannot be crashed), and an indirect cost per time unit set so that the optimum lies part-way along the crashing steps |
| Resources | A named resource, units per activity and a limit below the early-start peak, so levelling and scheduling within the limit both have something to show |
| Calendar | Start date Sunday 4 October 2026 with a Friday–Saturday weekend (the Weeks example has no dates) |
| Progress | % complete and actual cost at a status date about 40% into the project, a baseline saved on loading, and two earlier status records for the S-curves |
| Scenarios | *Base case (normal durations)* and *Crashed to the optimum*, created on loading |
| Target | A PERT target completion time |

The **Validation demo** keeps its circular dependency on purpose; once the cycle is fixed, its data works in every tab too. The **Relationships with lags** example uses SS/FF links, so it has no AOA diagram.

Two examples are built for the advanced tools:
- **PERT, costs and resources** (warehouse expansion): nine activities with hand-picked estimates and costs. It has two parallel critical paths, one of them through an activity that cannot be crashed, so it shows why crashing must cut every critical path.
- **Relationships with lags** (pipeline installation): excavation, pipe laying and backfill overlap through start-to-start and finish-to-finish links.

The same data is in the files in `examples/`, which also contain the baseline, status records and scenarios. Loading a file with **Import** gives the same project as clicking the example card.

## 12. Practice mode

**Practice** in the control bar hides every answer: the KPI values, completion time, Gantt chart, network, CPM table, analysis and status column. A practice table appears under the activity table. Students enter ES, EF, LS, LF, TF and FF for each activity, the project duration, and which activities are critical.

- **Check answers** marks each cell green (right), red (wrong) or dashed (not answered) and shows a score.
- For a wrong value the tool looks for the **misconception** behind it, by comparing the number with what typical mistakes produce (using the student's own neighbouring values and the correct ones). It names the concept, for example:
  - *"You used the smallest EF of the predecessors instead of the largest."*
  - *"You forgot that the activity has more than one successor: you used only 7, but activity 4 has 3 successors."*
  - *"You confused total float with free float."*
  - *"You added 1 to the predecessor finish (counting days inclusively)."*
  - *"You gave this end activity LF = its own EF."*, *"You used the successors' LF instead of their LS."*, *"You marked it critical because its free float is 0."*, *"You took the EF of the last activity in the table"* (for T).

  A **Misconceptions to review** box at the top groups them with how often each occurred and in which activities, so a student (or the instructor) sees the pattern, not only the wrong cells.
- Each wrong value gets a hint that names the rule and uses the student's own neighbouring values, for example *"Check the maximum of the predecessors' finish: ES = max(EF(2), EF(3)). With your values: max(9, 9) = 9."* or *"Your EF follows from your ES, so correct the ES first."* The hints also cover lags and SS/FF/SF links.
- **Show answers** fills in every value, **Clear** starts again and **Exit practice** shows the results.
- **Enter** in a cell moves down the column; on the last row it checks the answers.

## 13. AI assistant (optional)

The AI assistant is **off by default**, and the tool works fully without it. When it is on, it explains the schedule in plain language and answers questions about it, using the values the tool has already calculated.

**Turning it on:** click **AI assistant** in the control bar, tick **Turn on the AI assistant**, choose the provider (Claude by Anthropic, or OpenAI), check the model name, paste your API key and click **Save**. Keys come from [console.anthropic.com](https://console.anthropic.com/settings/keys) or [platform.openai.com](https://platform.openai.com/api-keys); usage is billed to that key.

- **Asking:** pick one of the suggested questions or type your own. In an activity's details panel, **Ask AI about this activity** explains that activity's times, float and status.
- **Accuracy:** the tool's engine does all the calculation, and the assistant is told to use those exact values. AI explanations can still be wrong, so check them against the step-by-step solution (section 7a).
- **Practice mode:** the assistant gives hints only. It is sent the activities, the student's entries and the misconceptions found by **Check answers**, never the correct values. Instructors can clear **Allow the assistant in Practice mode** in the settings for graded work.
- **Privacy:** while the assistant is on, the project data and your questions are sent to the chosen provider. Do not include personal or confidential information. The key is kept only for the current tab unless you tick **Remember the key on this device**; leave that off on shared or lab computers. **Forget key** removes it.
