# The Critical Path Method as implemented

This page describes exactly how the tool calculates the schedule, so that students can check every value by hand.

## Notation

| Symbol | Meaning |
|---|---|
| *d* | Duration of the activity |
| ES / EF | Earliest start / earliest finish |
| LS / LF | Latest start / latest finish |
| TF | Total float |
| FF | Free float |
| T | Project completion time |

## Step 1: Validation and cycle detection
Before any calculation, the tool checks every row. The network must be a directed acyclic graph: a depth-first search marks each activity as unvisited, in progress or finished. Reaching an activity that is still in progress means a cycle, which is reported (for example 3 → 5 → 7 → 3) and blocks the calculation.

## Step 2: Topological order
Activities are ordered with **Kahn's algorithm**: repeatedly take an activity whose predecessors have all been placed. Ties are broken by table row. The calculation therefore never depends on the order in which rows were typed.

## Step 3: Forward pass (in topological order)
- An activity with no predecessors: ES = 0
- Otherwise: ES = max(EF of all predecessors)
- EF = ES + *d*
- T = max(EF over all activities)

## Step 4: Backward pass (in reverse topological order)
- An activity with no successors: LF = T
- Otherwise: LF = min(LS of all successors)
- LS = LF − *d*

Setting LF = T for **every** end activity is what allows projects with several end activities.

## Step 5: Float
- Total float: TF = LS − ES = LF − EF
- Free float: FF = min(ES of successors) − EF, or T − EF for an end activity

Total float is how much an activity can slip without delaying the project. Free float is how much it can slip without delaying the earliest start of any successor.

## Step 6: Critical activities and paths
- An activity is critical when TF = 0 (a tolerance of 10⁻⁶ absorbs rounding with decimal durations).
- A link from P to S is critical when both are critical and EF(P) = ES(S).
- Every critical path is found by following critical links from each critical start activity (ES = 0) until an activity with EF = T is reached. All such paths are listed, so projects with parallel critical paths show each one.

## Worked example: New Product Development

| Activity | *d* | Pred. | ES | EF | LS | LF | TF | FF |
|---|---:|---|---:|---:|---:|---:|---:|---:|
| 1 Project Definition | 2 | – | 0 | 2 | 0 | 2 | **0** | 0 |
| 2 Requirements Analysis | 4 | 1 | 2 | 6 | 4 | 8 | 2 | 0 |
| 3 Concept Development | 5 | 1 | 2 | 7 | 2 | 7 | **0** | 0 |
| 4 Detailed Design | 6 | 2 | 6 | 12 | 8 | 14 | 2 | 2 |
| 5 Prototype Development | 7 | 3 | 7 | 14 | 7 | 14 | **0** | 0 |
| 6 Supplier Preparation | 4 | 2 | 6 | 10 | 12 | 16 | 6 | 0 |
| 7 Prototype Testing | 5 | 4, 5 | 14 | 19 | 14 | 19 | **0** | 0 |
| 8 Production Planning | 3 | 6 | 10 | 13 | 16 | 19 | 6 | 6 |
| 9 Final Validation | 4 | 7, 8 | 19 | 23 | 19 | 23 | **0** | 0 |
| 10 Project Launch | 2 | 9 | 23 | 25 | 23 | 25 | **0** | 0 |

- **T = 25 days**
- **Critical path:** 1 → 3 → 5 → 7 → 9 → 10 (2 + 5 + 7 + 5 + 4 + 2 = 25)

Two points worth discussing:
- Activity 7 has two predecessors, so ES(7) = max(EF₄ = 12, EF₅ = 14) = 14.
- Activity 2 has LF = min(LS₄ = 8, LS₆ = 12) = 8. Its total float is 2 but its free float is 0: any delay to activity 2 immediately delays activity 4's earliest start.

## Scheduling indicators
The analysis section reports:
- **Criticality ratio** = critical activities ÷ all activities
- **Schedule flexibility** = average total float
- **Potential bottleneck** = the longest critical activity
- **Near-critical activities** have 0 < TF ≤ 10% of T

**Risk level** is set by this rule:
- **High** when at least 60% of activities are critical, or at least 40% with more than one critical path.
- **Medium** when at least 35% are critical, or at least 30% are near-critical.
- **Low** otherwise.

These are rule-based indicators derived from the schedule, not statistical estimates of delay probability.
