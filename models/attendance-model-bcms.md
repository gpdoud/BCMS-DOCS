[Back to README.md](/README.md)

# Attendance Model (class)

## Overview

The `Attendance` model is used to track the student's attendance each day of the cohort. The attendance is designed for full-time cohorts that begin the day at 9:00 AM and end the day at 4:30 PM.

The `Attendance` model is linked to the `Enrollment` model.

In the morning a a full-time cohort day, the student must sign in to BCMS. They they should select the `CheckIn/Out` menu item which brings up a dialog. Normally, the student just clicks the `Check in` button to check-in for the day. At the end of the cohort day, the student logs into BCMS, selects the CheckIn/Out, then clicks the `Check out` button. 

When a student checks in for the day, an `Attendance` record is created and the date and time is recorded. At the end of the cohort day, the check out process will update the record created that morning and updates with the date and time the student checked out.

## Properties

The `In` property holds the date and time a student checked in.

The `Out` property holds the data and time a student checked out.

The `Excused` property is a boolean that indicates whether the student alerted the MAX Staff that the student would not be attending the cohort that day.

The `Absent` property indicates the student did not attend a normal cohort day. If the student did not notify the MAX staff, they student would not be excused.

- `Note` is a string property is where the student can add some text that the student either will be late for the cohort or will have to leave the cohort early.

- The `SecureNote` is a string property that the instructor or MAX staff that can document some information about the student. Students will never see this text info.
