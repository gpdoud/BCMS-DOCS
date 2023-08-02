[Back to README.md](/README.md)

# Creating Assessments (Evaluation & Questions models)

***Note: While this is called `Creating Assessments`, it is important to know that what is termed and`assessment` is actually using the `Evaluation` model and the `Assessment` model contains the scores from the Evaluations. It would be more correct if the `Evaluation` model name was changed to `Assessment` and the `Assessment` model name changed to `Score`.***

## Overview

Assessments are tests that students take throughout the cohort to evaluate their knowledge of topics taught. The assessments are multiple choice and true or false questions and have a time limit. Each question is given a point value usually 10 points. A question can be marked as a `bonus` question. Assessments are assigned to all students in a cohort. As soon as the student completes the assessment, their scores are registered in the `Assessmment` model. The student can review their assessment which will show each question, the possible answers, the student's answer, and the correct answer if the student's answer is wrong.

When students take an evaluation, they will see one question at a time. They will click their chosen answer then click the `Next` or `Prev` button to navigate to the next or previous question. Only when all questions have been answered will the `Done` button will display. Clicking that button will display another button `Verify Done if Finished`. Clicking this button will mark the evaluation done and add the score to the `Asmts` menu page.

## Creating an assessment (Evaluation)

To create an evaluation, the user must have admin or instructor in their role.

Click the `Eval(a)` menu item to display all the existing evaluations along with evaluations taken by students.

Click `Create` to display the `Evaluation Create` page.

* Fill in the `Description` with the name of the evaluation. The topic of the evaluation should be included.
* The `Points` are calculated based on the questions added later.
* Enter the time limit in minutes in the first textbox and seconds in the second. Use whole numbers only and not special characters like colons.
* Leave `Done?` unchecked. This is used only when a student takes the evaluation.
* Check the `Template` checkbox. This will allow it to be displayed when the `Evaluation List` page has the `Templates only` checked. Templates are those that can be assigned to students.
* The `Active` checkbox should be checked by default. Check it if it is not checked already.
* The `Owner` is readonly and will be filled with the logged in user when the add is done.

Click the `Save` button. Navigation will return to the `Evaluation List` page.

## Creating the questions

Once the evaluation is created, questions can be added.

From the `Evaluation List` page, click on the `Quests` action link. This will navigate to the `Questions List` page. This page will display all the questions for the selected evaluation.

Click on `Create` to navigate to the `Question Create` page.

* Fill in the `Category` which should include some identifier for the question. Something like, "Creating a git repo".
* Assign the `Point Value` as a postive, integer number.
* Enter the text for the `Question`.
* Add possible answers in the `A, B, C, D, E` textboxes. Only A & B are required. 
* Drop-down the `Answer` list and select the currect answer. Make sure the selected answer points to an answer that contains text. A & B are always displayed but C, D, and E are only displayed if they contain text.
* The `Is Bonus` defines the question as a bonus question. The point values for all non-bonus questions are added up to display the total points. Questions where `Is Bonus` is checked are NOT included in the total possible points.

Click the `Save` button. Navigation will return to the `Question List` page.

## Assigning an evaluation

From the `Evaluation List` page, check the `Templates Only` to display only evaluations that can be assigned to students.

* Click on the `Assign` action link to display the `Evaluation assign to cohort` page.
* Click on the `Cohorts` drop-down list and click on the cohort to assign the evaluation.
* Click on the `Display Students` like to display a list of all the students in the cohort.
* Each student in the list has a checkbox next to the name. To assign the evaluation to all the students, click the checkbox to the left of the `Student` column title. This will check all the students. Or individual student can be checked. This is useful when a single student might have to take a remedial evaluation.
* Once all the students are checked, click the `Assign to Selected Students`. This will place a copy of the evaluation in the student's `Eval` menu item.

***Note: If a student is displaying the `Eval` list before the evaluation is assigned, they page will not show the assigned evaluation. The student should simply navigate to another page then back to the `Eval` and it will refresh and the evaluation can be taken***