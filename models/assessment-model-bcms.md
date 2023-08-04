[Back to README.md](/README.md)

# Assessment Model (class)

## Overview

The `Assessment` model contains a collection the scores from evaluations taken by a student.

When an `Evaluation` is completed, BCMS will automatically add an `Assessment` that shows the score achieved on the evaluation. These `Assessments` are viewable by students immediately after completing the evaluation.

An `Assessment` is tied to the same `Enrollment` as the student.

## Properties

The `Date` is when the assessment was created (when the evaluation was finished).

`Subject` will be "Evaluation" when an assessment is created to record the score of an evaluation.

The `Description` will be the name of the evaluation.

`PointsMax` are taken from the evaluation.

`PointsScore` are the point awarded when questions are answered correctly.

