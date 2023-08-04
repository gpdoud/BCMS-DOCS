[Back to README.md](/README.md)

# Evaluation Model (class)

## Overview

The `Evaluation` model works with the `Question` model to provide the assessments that students must pass to graduate from the cohort.

***Note: It can be confusing that the tests taken by the students has been called an "Assessment" but actually refers to an `Evaluation`. To make matters more confusing, there is a model called `Assessment` that actually contains the scores from the `Evaluation`.***

`Evaluations` check the student's knowledge of a major topic within the cohort. In the coding boot camp, there are five evaluations that must be passed (minimum of 80 points). They are:

1. Git & GitHub
2. SQL
3. C#
4. Html, Css, JavaScript
5. Angular

If a student fails to achieve the 80 points required on an evaluation, instructors can create remedial evaluations on the same topic with differnt questions.

## Properties

The `Description` is the name of the evaluation like "Git & GitHub".

`IsTemplate` when checked, defines the evaluation as one to be assigned to students. The an evaluation is assigned, BCMS creates a copy of the then current evaluation and links the copy to a particular student.

The `IsDone` is a boolean value that is set when the student finishes the evaluation.

`PointsAvailable` contains the number of points available (excluding bonus questions) and `PointsScored` contains the number of points achieved by correctly answering questions.

`TimeLimitMinutes` and `TimeLimitSeconds` defines the amount of time to finish the evaluation. When that time expires, any unanswered questions will be considered wrong. This was added when some virtual students were taking an extraordinary amount of time to complete an evaluation at home *(i.e. one student took almost 20 minutes to finish a 10 question evaluation when most students finish in less than five minutes)*.