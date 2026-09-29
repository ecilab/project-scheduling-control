# Changelog

## [1.1.0] – 2026-09-29

### Scheduling engine
- Precedence relationships FS, SS, FF and SF with lags and leads (`4SS+2`, `3FF`, `5FS-1`, `4+2`), in the forward and backward pass, free float and critical-path search.
- Working-day calendar: start date, weekend pattern, holidays; dates in the Gantt axis, tooltips, CPM table, details panel and exports.

### Analysis tools
- PERT: three time estimates, expected times, path variance, P(T ≤ target) and the duration for a required probability.
- Monte Carlo simulation (Beta-PERT or triangular, seeded) with the completion-time distribution, percentiles and criticality index.
- Crashing: minimum-cost crashing step by step (minimum cut across parallel critical paths), direct, indirect and total cost curves and the optimum.
- Resource histogram, levelling within float (Burgess) and resource-limited scheduling.
- Baseline, progress tracking and earned value (PV, EV, AC, SV, CV, SPI, CPI, EAC, ETC, VAC, TCPI, earned schedule) with S-curves; baseline bars and progress shading on the Gantt chart.
- What-if scenarios saved with the project and compared side by side; any crashing step can be saved as a scenario.

### Teaching
- Student practice mode that hides the answers, marks each ES, EF, LS, LF, TF, FF and critical flag, and gives rule-based hints.
- Misconception diagnosis in practice mode (min instead of max, ignored predecessors or successors, ES/EF and LS/LF mix-ups, adding 1, end-activity LF, total vs free float, criticality by free float, T errors), with a summary by misconception.
- Step-by-step worked solution with actual numbers, animated on a copy of the network, per-activity lines in the details panel, and a printable model answer sheet.
- Activity-on-arrow diagram with the minimum dummy activities and event times.
- Two new examples: warehouse expansion (PERT, costs, resources) and pipeline installation (SS / FF lags).
- Every example now carries PERT estimates (with te equal to the original durations), costs and crash data, resources with a limit, a calendar, progress, and on loading a baseline, status history and two scenarios (base case and crashing optimum).

### AI assistant (optional)
- Off by default. With the user's own Claude (Anthropic) or OpenAI API key, explains the calculated schedule and answers questions; an **Ask AI about this activity** button in the details panel.
- The engine does the maths and the model is given the exact values; in Practice mode it gives hints only and is not sent the correct values, and it can be turned off for graded work.
- The key is kept in sessionStorage unless the user chooses to remember it; privacy statements in the README and NOTICE updated.

### Interface
- Layout adapted for phones and tablets: one swipeable control row, a compact two-column KPI grid, larger touch targets, 16px inputs (no zoom on focus in iOS), and export menu, drawer and toasts sized for small screens.
- Language and theme switches moved to the upper corner of the header.
- Network diagram at actual size, in AON and AOA, is centered in its frame; Fit to width now also works for AOA.
- Fixed buttons marked hidden still showing (for example Animate Critical Path in AOA mode).

### Import and export
- Excel workbook (.xlsx) with live CPM formulas and sheets for PERT, crashing, resources, earned value and Monte Carlo.
- MS Project XML (MSPDI) with links, lags, calendar, costs, progress and resource assignments.
- Optional CSV columns for PERT estimates, costs, resources and progress; JSON now also stores the calendar, baseline and scenarios.

## [1.0.0] – 2026-09-27
First public release.

### Scheduling engine
- Validation of activity numbers, names, durations and predecessor formatting.
- Cycle detection by depth-first search, with the exact cycle reported (for example 3 → 5 → 7 → 3).
- Kahn topological sort, forward pass, backward pass, total float and free float.
- Support for several start and end activities, zero-duration milestones and decimal durations.
- Enumeration of every critical path, not only the first one found.

### Interface
- English / Arabic with full right-to-left layout.
- Light and dark themes.
- Animated Gantt chart with dependency arrows, float tails, critical-path tracing and schedule playback.
- Activity-on-node network diagram with an animated critical-path run.
- Illustrated KPI cards, CPM table and a generated schedule analysis with risk indicators.
- Five built-in examples: product development (10 activities), two critical paths (11), medium (20), large (40) and a cycle validation demo.
- Import and export as CSV and JSON, Gantt export as PNG, and a printable report.
