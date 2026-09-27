# Changelog

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
