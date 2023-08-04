[Back to README.md](/README.md)

# CalendarDay Model (class)

## Overview

The `CalendarDay` model works with the `Calendar` to support the calendar function for a cohort. Every `CalendarDay` row is related to a `Calendar` and represents a day between the start date and graducation date of the cohort. Each day will either be a class day or a non-class day.

### Properties

The `Date` defines the day of the cohort. There will be one row for every cohort day.

The `Topic` and `Subtopic` detail what is planned for that particular day.

The `WeekNbr` defines the week of the cohort which will be from one to the number of weeks of the cohort and the `DayNbr` identifies the day of the cohort. 

The `NoClassToday` when checked means there is no class on that date.

The `AssessmentToday` is a string where the assessment to be administered on that day is entered. When a student displays the `Schedule` menu items, days where `AssessmentToday` exists will display with a reddish colored background.