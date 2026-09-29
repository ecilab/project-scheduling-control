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

## Relationship types and lags (precedence diagramming)

For a link from predecessor P to successor S with lag *L* (negative for a lead), the forward pass takes ES(S) as the largest of 0 and:

| Type | Constraint on S |
|---|---|
| FS | ES(S) ≥ EF(P) + *L* |
| SS | ES(S) ≥ ES(P) + *L* |
| FF | EF(S) ≥ EF(P) + *L*, so ES(S) ≥ EF(P) + *L* − *d*(S) |
| SF | EF(S) ≥ ES(P) + *L*, so ES(S) ≥ ES(P) + *L* − *d*(S) |

The backward pass mirrors it: LF(P) is the smallest of T and, for each successor, LS(S) − *L* (FS), LS(S) − *L* + *d*(P) (SS), LF(S) − *L* (FF) or LF(S) − *L* + *d*(P) (SF). Free float is the smallest gap on the outgoing links, and a link is critical when both ends are critical and its gap is 0.

## PERT

- *te* = (*a* + 4*m* + *b*) / 6 and σ² = ((*b* − *a*) / 6)²
- The project duration T is the CPM duration with *te* as the activity durations.
- σ²(T) = the sum of σ² along the critical path. With several critical paths, the path with the largest variance is used.
- *z* = (target − T) / σ(T) and P(T ≤ target) = Φ(*z*), the standard normal distribution.
- The duration with probability *p* of being met is T + Φ⁻¹(*p*) · σ(T).

**Warehouse example:** T = 29 days along 1 → 3 → 4 → 6 → 8 → 9, σ² = 0.11 + 2.78 + 0.44 + 1.78 + 1.78 + 0.11 = 7.00, σ = 2.65. For a target of 31 days, *z* = 2 / 2.65 = 0.76 and P = 77.5%.

## Monte Carlo simulation

Each run draws every uncertain duration independently (Beta-PERT with shape parameters α = 1 + 4(*m* − *a*)/(*b* − *a*) and β = 1 + 4(*b* − *m*)/(*b* − *a*), or triangular), then runs the full forward and backward pass. The criticality index of an activity is the share of runs in which its total float was 0. The random generator is seeded, so the same seed repeats the same runs.

## Crashing

- Cost slope = (crash cost − normal cost) / (normal duration − crash duration).
- Each step finds the cheapest set of critical activities that shortens every critical path: a minimum cut in the critical network, where each activity is an arc with capacity equal to its slope (infinite when it is at its crash limit). Reverse arcs of infinite capacity make each critical path cross the cut exactly once.
- The step length is 1 time unit, or less when an activity reaches its crash limit or a non-critical path runs out of float first.
- Direct cost = Σ normal costs + Σ slope × time crashed. Indirect cost = indirect rate × T. The optimum is the duration with the lowest total.

**Warehouse example** (indirect cost 1,200 per day): step 1 crashes activity 1 (slope 1,000, on both critical paths). Step 2 crashes activity 6 (1,000) by one day, when activity 5 becomes critical. Steps 3–4 crash activity 8 (1,200), which is cheaper than crashing 5 and 6 together (1,800). Durations 27, 26 and 25 all cost 82,400 in total. Activity 3 cannot be crashed, so once activities 1, 4, 6, 8 and 5 are exhausted the project stops at 22 days.

## Resource levelling

- The histogram is the sum of the units of all activities in progress at each moment.
- **Levelling** (Burgess method) moves non-critical activities, from the latest to the earliest, to the start within their current feasible window that gives the smallest Σ r² · Δt, and repeats until nothing moves. The project duration is unchanged.
- **Within limit** is a serial schedule: the eligible activity with the smallest LS is placed at its earliest start at which the demand never exceeds the limit.

## Earned value

For each baseline activity with budget BAC*i*, planned from ES to EF:

- PV(t) = Σ BAC*i* × min(1, max(0, (t − ES) / (EF − ES)))
- EV = Σ BAC*i* × % complete, AC = Σ actual cost
- SV = EV − PV, CV = EV − AC, SPI = EV / PV, CPI = EV / AC
- EAC = BAC / CPI, ETC = EAC − AC, VAC = BAC − EAC, TCPI = (BAC − EV) / (BAC − AC)
- Earned schedule ES*t* is the time at which PV reaches EV; SPI(t) = ES*t* / t and the forecast duration = planned duration / SPI(t).

## Activity-on-arrow diagram

1. Each distinct set of predecessors gets a start event, and each activity gets its own end event, joined by dummy arrows.
2. Dummies implied by another path are removed.
3. The two events of a dummy are merged when one of them has no other arrow on that side, unless the merge would give two activities the same pair of events.
4. Events are numbered level by level; the earliest and latest event times come from a forward and backward pass over the arrows.
