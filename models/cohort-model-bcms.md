[Back to README.md](/README.md)

# Cohort Model (class)

## Overview

The `Cohort` model is one of the most important models in BCMS. It represents a class or cohort. It defines the start, end, and graducation dates, the instructor(s) that will be teaching, and the calendar that outlines the curriculum for the cohort.

Students must be enrolled in a cohort so they can take the assessments (evaluations), have their scores reported, and have their attendance tracked.

***Note: It is important that a student be enrolled in only one active cohort at a time.***

## Properties

There is the `InstructorId` property that is no longer used.

The `Capacity` is a reference defining the suggested, maximum number of students. This field does NOT limit the number of students that can be enrolled

The `VirtualSession` is not used at this time. It was designed to provide a link to a virtual session (like Zoom) that would start up automatically.

The `UserId` is a foreign key to the user that created the cohort.