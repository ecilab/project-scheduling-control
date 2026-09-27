# Exercise answers

All values below were produced by the tool's own CPM engine. Remove this file from a public copy if the exercises are used for assessment.

## A. New Product Development

**A1.** T = 25 days. Critical path: 1 → 3 → 5 → 7 → 9 → 10.

| Act. | *d* | ES | EF | LS | LF | TF | FF |
|---|---:|---:|---:|---:|---:|---:|---:|
| 1 | 2 | 0 | 2 | 0 | 2 | 0 | 0 |
| 2 | 4 | 2 | 6 | 4 | 8 | 2 | 0 |
| 3 | 5 | 2 | 7 | 2 | 7 | 0 | 0 |
| 4 | 6 | 6 | 12 | 8 | 14 | 2 | 2 |
| 5 | 7 | 7 | 14 | 7 | 14 | 0 | 0 |
| 6 | 4 | 6 | 10 | 12 | 16 | 6 | 0 |
| 7 | 5 | 14 | 19 | 14 | 19 | 0 | 0 |
| 8 | 3 | 10 | 13 | 16 | 19 | 6 | 6 |
| 9 | 4 | 19 | 23 | 19 | 23 | 0 | 0 |
| 10 | 2 | 23 | 25 | 23 | 25 | 0 | 0 |

**A2.**
- (a) T = 26 days.
- (b) Critical path: 1 → 2 → 4 → 7 → 9 → 10.
- (c) Activity 2 had 2 days of total float, so the first 2 days of the 3-day delay are absorbed. Only the remaining day reaches the finish.

**A3.** No, T stays 25 days. Activity 6 has 6 days of total float, and a 5-day delay is within it.

**A4.**
- (a) T = 23 days.
- (b) Two critical paths: 1 → 3 → 5 → 7 → 9 → 10 and 1 → 2 → 4 → 7 → 9 → 10.
- (c) No. The path through activities 2 and 4 now has the same length (23 days), so it also sets the finish. Shortening activity 5 further does not shorten that path.

## B. Production Line Installation

Base schedule: T = 45 days. Critical path: 1 → 2 → 4 → 6 → 9 → 12 → 13 → 17 → 19 → 20.

**B1.** 10% of 45 = 4.5 days. Near-critical activities:
- 3, 5, 7 and 11 (TF = 1)
- 18 (TF = 3)
- 8 (TF = 4)

**B2.** Activities 3, 5, 7, 8 and 14 have total float but zero free float. Any delay to one of them immediately pushes back the earliest start of a successor, and it uses up float that is shared with the rest of its path.

**B3.** T = 44 days. New critical path: 1 → 3 → 5 → 7 → 11 → 12 → 13 → 17 → 19 → 20. The procurement chain (3 → 5 → 7 → 11) had only 1 day of float. After 1 day of saving it becomes critical, so the second day is not gained.

**B4.** T = 46 days. The procurement chain had 1 day of float, so a 2-day delay adds 1 day, and that chain becomes the critical path.

## C. Validation demo

**C1.** The cycle is 3 → 5 → 7 → 3: activity 3 depends on 7, 7 depends on 5, and 5 depends on 3. None of them can start first, so there is no topological order and ES cannot be calculated.

**C2.** T = 15 days. Critical path: 1 → 3 → 5 → 7 → 8.

## D. Smart Factory Construction

Base schedule: T = 149 days. The two critical paths are:
- 1 → 2 → 5 → 7 → 9 → 10 → 11 → 12 → 13 → 14 → 15 → 16 → **17 → 18** → 26 → 27 → 28 → 30 → 32 → 37 → 38 → 39
- 1 → 2 → 5 → 7 → 9 → 10 → 11 → 12 → 13 → 14 → 15 → 16 → **23 → 25** → 26 → 27 → 28 → 30 → 32 → 37 → 38 → 39

**D1.** They split after activity 16 (Structural Frame) and join again at activity 26 (Interior Partitions). Roof + envelope (6 + 10) and electrical rough-in + fire protection (10 + 6) both take 16 days.

**D2.** No, T stays 149 days. The branch through 17 and 18 is still 16 days long and still controls the finish; only one critical path remains. Shortening one of two parallel critical paths gives no saving.

**D3.** T = 147 days. Activity 16 lies on both critical paths, so shortening it shortens both.

**D4.** Every activity without successors gets LF = T (149). Activity 40 (Landscaping & Parking) therefore gets LF = 149 even though its EF is only 103, giving it 46 days of total float.
