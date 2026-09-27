# Exercises

These exercises use the built-in example projects. Load an example from the cards above the activity table, work out the answer by hand first, and then change the table to check your result in the tool.

Answers: [`exercises-answers.md`](exercises-answers.md) (your instructor may remove this file).

## A. New Product Development (10 activities)

**A1. Full CPM by hand.** Before loading the example, draw the network and complete the forward and backward passes for all ten activities: ES, EF, LS, LF, total float (TF) and free float (FF). State the completion time and the critical path. Then load the example and compare.

**A2. A delay beyond the float.** Activity 2 (Requirements Analysis) takes 7 days instead of 4.
- (a) What is the new completion time?
- (b) What is the new critical path?
- (c) Why is the project delayed by 1 day and not by 3?

**A3. A delay within the float.** Activity 6 (Supplier Preparation) takes 9 days instead of 4. Does the completion time change? Explain using its total float.

**A4. Crashing.** Activity 5 (Prototype Development) is shortened from 7 to 5 days.
- (a) What is the new completion time?
- (b) How many critical paths are there now, and which are they?
- (c) Would shortening activity 5 to 4 days save a further day? Why or why not?

## B. Production Line Installation (20 activities)

**B1. Near-critical activities.** List every activity whose total float is greater than 0 but at most 10% of the project duration.

**B2. Total float vs. free float.** List the activities that have total float but **zero** free float. What does a delay in one of them do to its successors?

**B3. Crashing civil works.** Activity 6 (Civil Works) is shortened from 8 to 6 days. What is the new completion time and critical path? Why is the saving smaller than 2 days?

**B4. Supplier delay.** Activity 7 (Equipment Procurement) takes 12 days instead of 10. What is the new completion time?

## C. Validation demo (circular dependency)

**C1.** Load the validation demo. Which activities form the cycle, and why can CPM not be calculated?

**C2.** Remove activity 7 from the predecessors of activity 3 (leaving `1`). What are the completion time and the critical path?

## D. Smart Factory Construction (40 activities)

**D1.** The project has two critical paths. Where do they split and where do they join again?

**D2.** Activity 23 (Electrical Rough-in) is shortened by 1 day. Does the completion time change? Explain.

**D3.** Activity 16 (Structural Frame) is shortened from 15 to 13 days. What is the new completion time? Why does this change help when D2 did not?

**D4.** The project has two start activities (1 and 4) and two end activities (39 and 40). How does the backward pass treat the two end activities?
