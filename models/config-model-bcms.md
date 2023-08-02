[Back to README.md](/README.md)

# Config Model (class)

## Overview

The `Config` model is a collection of key/value pairs used to manage BCMS. The `KeyValue` property is a unique identifier for the configuration and the `DataValue` is the value for the key. Both the key and value are strings.

The `KeyValue` can be up to 50 characters but should include only letters, numbers, and periods and should be all lowercase.

## Properties

Some `Config` items are more significant than others.

### No class dates

There are an important set of config items that are used in support of the Calendar & CalendarDay models. These are items whose keyvalue must begin with `noclassdate` plus any other data. These represent days in a calendar that should not have cohort classes scheduled. Here is an example of one of these items that define September 4, 2023, Memorial Day as a NO CLASS day.

    KeyValue: noclassdate.20230904.memorialday, DataValue: 9/4/2023

Any characters after `noclassdate` are ignored and are only for the users to identify its purpose. The data value must be a valid date in m/d/yyyy format. ***It is important that the full year is included in the date.***

### Messages

In the upper right of the header on the BCMS pages is a short text message displayed to users. These short text messages are taken from the config items that have key values that start with `notify`.

    KeyValue: nodify.0, DateValue: BCMS is running in Azure

All of these key values are read into BCMS when a user logs in and all the data values are displayed at the top of the page. It is not well known that if a user clicks on one of these messages, they will rotate to display the next message. After the last one is displayed, the first to be displayed again. They are displayed in thee order they exist on the list page.

### Display only

Here is a list of the keys and their use. These are all items that are displayed on one or more pages.

| KeyValue  | Usage |
| ---       | ---   |
| author       | Author's name   |
| copyright | Copyright information |
| name  | Application name |
| rights | Additional copyright information |
| status | Status of the current deployment software |
| version | Version of currently deployed software |
| version.date | Date current version was deployed |
