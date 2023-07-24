[Back to README.md](README.md)

# Calendars

## Overview

For many years, the coding boot camp defined the daily curriculum on a spreadsheet. It detailed what topic and who the instructor was. Once the curriculum was finalized, a copy of the spreadsheet was distributed to the students and instructors. Most of the time, this process worked just find.

Issues started when the curriculum had to be changed because of guest speakers needing to move the date because of some conflict or any other reason. The curriculum was changed and distributed to *some* but not *all* those involved. The result was that students were told by one staff member that tomorrow X would happen while a different staff member might tell them that Y was happening. It projected some confusion and disarray to students about the MAX process.

To address this issue, an enhancement to BCMS was suggested. It asked to create a calendar for each cohort, there would be one version of the "truth" as to what was planned for each day of the boot camp and if something had to change, all involved would see the changes.

## How it works

Two new tables were added to BCMS: `Calendars` and `CalendarDays`. 

The Calendar table's major properties are the `StartDate` and `Type`. 

The `StartDate`` defines the date for the first day of a cohort.

The `Type` defines whether the calendar is for the full-time `FT` or part-time `PT` boot camp. The Type is needed so that the days of the week can be loaded properly since the days for the full-time boot camp is Monday thru Friday and the part-time boot camp is Monday, Wednesday, and Saturday. 

There is a property called `Template` which is designed to be a typical calendar that can be copied for the full-time or part-time boot camp. When a calendar is marked as a template, new calendars can be created by having BCMS copying the template calendars.

Because calendars are tied to cohorts, the `Cohorts` table needed to be modified to hold an optional (nullable) foreign key to the calendar.

When a cohort is connected to a calendar, the students enrolled in that cohort can click on a menu item called **Schedule** and view the calendar for their cohort showing the topic, instructor, an assessment, and other items scheduled for that day.

The `CalendarDays` table has a foreign key to the `Calendars` table. Each `CalendarDays` row defines a single day.

The `Date` is the day within the cohort.

There is a `Topic` and optional `Subtopic` that defined what is scheduled for that day.

The `WeekNbr` displays the week of the boot camp and the `DayNbr` displays a sequential number starting at 1 and ending with the number of days in the particular boot camp.

`AssessmentToday` is for entering the assessment that the students will be taking on that day. Otherwise, it is left blank.

`GraduationToday` it set to *true* for the one day when graduation occurs.

`NoClassToday` if set to *true* means the cohort does not have hold class on that day.

## Creating a Calendar for a Cohort

There are two ways of creating new calendars: 1) creating each day from scratch and 2) copying an existing calendar.

### Creating a calendar from scratch

Creating a calendar by manually adding the calendar then adding all the calendar days is a very tedious process. It may be required if a new cohort is created and has a different number of day from any existing calendar. Except for small cohorts, this it not the recommended way to create a new calendar.

### Creating a calendar by copying

Copying an existing calendar then modifying the new calendar is a much better way of creating a new calendar.

In the Calendar List at the top of the page is a **Clone** link. This will begin the process of copying a calendar.

The Calendar Clone page will take only three steps.

#### Step 1 - Select an existing calendar

The drop-down list will display all the active calendars currently available. Select the calendar that most closely represents the new calendar to be created.

#### Step 2 - Select the starting date

Because the selected calendar probably has a different starting date then the new calendar, this field defines the starting date of the new calendar. When the selected calendars is copied, the first day of the selected calendar will become the first day of the new calendar but the date of that first day will be the date provided in this fields. Cloning will only put selected calendar days on the appropriate days in the new calendar. 

For example, if a selected calendar for a full-time boot camp started on a Monday but the start date of the new calendar is a Wednesday, the fourth day of the selected calendar, which was on a Thursday will be moved to the next Monday of the new calendar.

Once the new calendar is created, it is likely that some of the individual dates must be changed to accommodate instructor's schedules.

## Making changes to calendars

For both the calendar and calendar days, individual row can be created, modified, and removed just like all other rows.

*Note: When a calendar is attached to a cohort, that calendar cannot be deleted without removing the calendar from any and all cohorts.*

***Important Note: A calendar CAN be deleted even when it has CalendarDays attached to it. Deleting the calendar will also delete all the calendar days attached to it.***

Most of the changes required on a new calendar that has been cloned is to individual days within that calendar. For example, in the full-time boot camp, the 2 days of SCRUM training held on days 35 & 36 may need to be moved to days 27 & 28 of the new calendar. This is likely the same for the 2 days of hosting.

### Calendar days using actions UP (UP) and DOWN (DN)

To handle the movement of days like the SCRUM and Hosting, each calendar day has an ACTION of `UP (Up)` and `Down (Dn)`. When UP is clicked, the current day is swapped with the previous day on the calendar. When DN is clicked, the current day is swapped with the next day on the calendar. Specifically, the `Date`, `WeekNbr`, and `DayNbr` properties are swapped.

## Security

At the present time, only users with administrative privilege can maintain the calendars.
