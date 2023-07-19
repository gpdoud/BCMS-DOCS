# Boot Camp Management System (BCMS)

This is a high-level overview of the BCMS system used to manage the MAX Technical Training boot camps. More detailed information will be provided in other blog posts.

As of July 18, 2023, BCMS is hosted on Greg’s hosting provider (Winhost) and is accessible at http://doudsystems.com/bcmsng.

This will start with an overview of the features of BCMS.

## Logging in

As is the case with many websites, users must log into BCMS with a username and password both of which are provided to the valid users. The default username is the first initial of the first name concatenated with the entire last name. So a username for “Jane Doe” would be “jdoe”. The password defaults to the standard MAX password “Train@MAX”. The user can change either or both of their username and password by logging in and clicking on their username on the right side of the menu.

A user profile can be disabled by unchecking the ACTIVE checkbox. This will prohibit the user from logging into the system.

BCMS does supports restrictinging a remote student from logging into BCMS from an IP address not stored in a collection within BCMS. The features is completely disabled at this time.

To reenable the IP checking feature requires changing the `config.json` file in the `src/assets/` folder for the DsiBcmsClient project. The `checkIp` must be set to `true` and the `validIps` must have an item added with any name and the specific IP address that will be allowed to connect to BCMS.

## User profile

The user profile has a number of traditional data items like:

* First and last name
* Username and password
* Email and phone number (home and work)
* Active indicator
* Role (see Roles)
* Security Key (Not used at this time)
* Created (date created - readonly)
* Updated (last date updated - readonly)

The only sigificant data in the profile is the `active` which allows the user to login and the `role` which defined the capabilities of the user.

## Roles (Security)

Roles define the capabilities of the user. Each user is related to a single role but roles can define capabilities for more than one role.

### Root

The `root` role is the highest security level. There are no restrictions on the root user.

### Admin

The `admin` role permit the user to do setup on the cohort, add users, and enroll users into the cohort, and monitor check-ins.

### Staff

TBD

### Instructor

The `instructor` role allows the instructor to maintain create and modify evaluations (assessments), assign them to students within the cohort, and modify evaluation (assessment) scores if needed.

### Student

The `student` role limits a user to simply logging in, checking in and out, and taking the evaluations (assessments)

## Home page

The home page has recently been converted to a help page for students and admin/staff. It describes for students how to check-in, take evaluations (assessments) and review the scores. For admin, it describes how to add users to BCMS, adding cohorts, enrolling students in cohorts, viewing a students scores, and reviewing student attendance. 

## Checking in and out

BCMS was initially created to address this issue. Instead of students signing a sheet of paper when they come in and leave a class, which was forgotten many times, BCMS will keep track of the comings and going of student in a cohort.

After logging into BCMS, student simply click the `CheckIn/Out` menu it. The student will see a dialog that tell them whether they are currently checked in or out. It also include a textbox for a note. This is used if the student has checked-in late or has to leave early for some reason. The button face will show `Check in` or `Check out` based on whether the student is currently checked in or out.

When student check in or out, it is recorded in the database. 

## Cohorts

`Cohorts` represent classes. They include the name of the cohort, the planned start, end, and graducation dates, the capacity of the class along with the number of students currently enrolled in the class, and whether the cohort is active or not. 

Inactive cohorts do not display by default but can be displayed by clicking the `Show inactive` checkbox at the top of the page.

Cohorts can be maintained by the `instructor`s assigned to the cohort or by `root`, `admin`, or `staff`.

The `Actions` for a cohort support displaying the student's attendance, displaying student scores, viewing the check-in or out status of students, enrolling or dropping students from a cohort, adding instructors, or modifying the cohort itself

### Check-in/out report (Rpt)

Student check-in and out of class every day. This is recorded in the database. then clicking on `rpt` next to the cohort to display. The report shows the date, the check-in and check-out time and any notes along with the `Excused`, `Absent`, and `Secure Note` which are properties that can only be set by an `instructor`, `admin`, or `root` user.

### Displaying student scores (Asmts)

This displays all the evaluations (assessments) scores for all the students in the cohort.

Using the `Search` at the top of the page, the display can be limited to only those rows that contain the substring entered in the search box.

### Monitor check-in and out status (ChkIO)

This will help the instructor or staff to monitor the status of all the students as to whether they are checked-in or out.

The page shows a box (button) for each student. The box is color coated indicating whether the student is checked-in or checked-out. If the box is grey, it indicates the student is checked out. If the student is checked-in on time, the box will be green. If the student has checked in late, the box will be yellow. This late check-in applies only to the full-time cohorts that start class at 9 AM.

If a student notifies that (s)he will not be attending class on a particular day (for whatever reason), the instructor or admin/staff can check the student in and out by clicking the box.

### Enrolling students (Enrll)

This page supports enrolling and dropping student from a cohort.

It shows the specific cohort selected at the top and include the capacity and current number of enrolled students. Next comes a list of the students that are currently enrolled in the cohort followed by a list of students not currently enrolled in the cohort.

To enroll a student, click the green `Enroll` like next to the student's name. To drop a student, click the red `Drop` link next to their name.

_Note: Currently BCMS does NOT exclude students that are enrolled in other cohorts from the list of student can can be enrolled. A student already enrolled in a cohort should not be enrolled in another cohort._

## Assigning instructors (Inst)

This is a new function of BCMS. Not multiple instructors can be assigned to a cohort. This is to support cohorts where different instructors will be teaching. Each instructor has full instructor rights to management the cohort they are assigned to.

_Note: The assignment of instructors must be done after the cohort is created._

## Evaluations (Assessments)

In the coding boot camps, student are required to take and pass multiple tests. These tests have been called 'assessments' by most staff but in BCMS, the test are `Evaluations` and the scores for the tests are `Assessments`.

For students, there is only one menu item for Evaluations. The `Evals` is for students to _take the tests_ and _display the results_. 

The `Evals(a)` is visible only for instructors and admin/staff to maintain and review the evaluations and scores themselves.

- The `Description` is the name of the evaluation
- The `Points` display the total points and the number of points scored. 
- The `Done?` indicates whether a student has finished the evaluation.
- The `Template?` is the evaluation that will be assigned to students.
- The `Active` will hide the evaluation from display if unchecked
- The `Owner` is the user that created the evaluation

Once a student finishes an evaluation, the `Action` changes to `Review` from `Take`. Clicking `Review` will display all the questions and answers of the evaluation. Questions answered correctly will be displayed in green. Questions answer incorrectly or not answered will be displayed in red and the correct answer will be displayed in green. In addition, the score for the evalution will be added to the Assessments page automatically.

### Questions (Quest)

An evaluation is a multiple choice or true/false test with a number of questions with each questions haveing from 2 to 5 possible answers where only a single answer is correct. Each question has a point value and it is awarded if the question is answered correctly.

There are normal questions and there are bonus questions. The point values of normal questions are added to the sum total for the test so 10 questions each with a point value of 10 points means the entire test totals 100 points. A bonus question is NOT added to the total but allows the student to score the point value. So if a bonus question is added to the previous 10, the total value is still 100 but answering all 11 questions correctly would score a 110 points.

Each question must be added individually. 

- The `Category` is only for reference and it not significant. 
- The `Point Value` sets the number of points for the question.
- The `Question` is what will be displayed to the student.
- The `A - E` textboxes are the possible answer to the question. _A and B are required_
- The `Answer` drop-down indicates the correct answer.
- The `Is Bonus` checkbox indicates whether this questions is a bonus or not.

### Assigning Evaluation to students (Assign)

This action of the `Evals(a)` is to assign an evaluation to an entire cohort or to specific student within a cohort.

When selected, the name of the evaluation will be displayed alongside a drop-down list of active cohorts. Selecting a cohort will reveal a link to `Display Students`. Clicking this link will display all the students enrolled in the chort with a checkbox next to their name. To assign the evaluation to all students, click the checkbox to the left of the `Student` header. This will place a check on all the students. Or check the box next to any or all students directly.

When all the students are checked, click the red link `Assign to Selected Students` and a message will be displayed for all the students assigned. Each assigned student should see the evaluation display in their `Eval` menu item. If it is not displayed for a student, the student should navigate to another menu item and navigate back to `Evals`.

## Assessments (Scores)

The `Asmts` menu displays the scores for a student's evaluations. It is a display-only page. When an evaluation is completed, BCMS will automatically add the score to this page.

## Configs (Configuration)

`Configs` was created to provide an easy way to control BCMS without having to continually add new tables to the database. Additional config row can be added anytime using any key and value. There are methods in the controller that allows accessing one or multiple config records with one call.

The `Configs` are accessible only to `root` or `admin/staff`. The data is structured in a collection of key/value pairs. Most of the items are for display purposes only but a few are more significant.

Here are the more significant ones:

- `late.hour` & `late.minute` used together, this is the time afterwhich a student is considered late for class

These are mostly for display:

- `author` original author of BCMS
- `copyright` years that copyrights apply
- `name` official name of the product
- `notify.X` a collection of messages displayed at the top right of the header where 'X' is a sequential number to sequence the messages
- `rights` displays "RESERVED" along side copyright
- `status` displays the version and status of the deployed product
- `version` version number
- `version.date` the date the version was created

## KB & KBCategory

The `Kb` was designed to allow student to enter questions that could answered and made available to all students to solve problems. The `KbCategories` where used by the `Kb` to categories the question like `C#`, `Angular`, or `SQL Server`. 

This feature has not be utilized much over the years.

After a question was entered and a response provided, the KB could be locked so that it can be read by students but not changed. Instructors, admin and staff can always change a Kb.

## Logs

BCMS has its own log file where messages from code can be stored in the log and is accessible to non-students from the BCMS menu. Most of the logging today is recording the logging in and out of BCMS by all users. The log table grows quickly and should manually be purged of older log records.
