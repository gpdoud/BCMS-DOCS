[Back to README.md](/README.md)

# Calendar Model (class)

## Overview

The `Calendar` model is the primary model that supports that calendar function for cohorts. It works with the `CalendarDay` model to provide the complete calendar function.

## Properties

The `Calendar` has a number of important properties.

The `StartDate` of a cohort is used when a calendar is ***cloned*** meaning it is created by copying the calendar days from another calendar.

The `Tyoe` identifies the calendar as either a full-time (FT) or part-time (PT). This is important because a full-time cohort has class days Monday thru Friday and a part-time cohort has class days on only Monday, Wednesday, and Saturday. The `Type` property tells the cloning process which days of the week can contain class days.

The `Tenplate`, when set to `true` means it exists to be cloned to create new calendars rather than being assigned to a cohort. The cloning process can use a template calendar or a non-template calendar.

