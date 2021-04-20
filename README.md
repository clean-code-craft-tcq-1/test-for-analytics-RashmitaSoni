# Test for Analytics

Design tests for Analytics functionality on a Battery Monitoring System.

Fill the parts marked '_enter' in the **Tasks** section below.

## Analysis-functionality to be tested

This section lists the Analysis for which _tests_ must be written.

Battery Telemetrics are collected and stored on a server.
Data for a month is stored in a [csv file](https://en.wikipedia.org/wiki/Comma-separated_values).

Analysis must be done on this csv file to find the following:
- minimum
- maximum
- count of breaches (how many times did it cross the threshold in a month?)
- record trends (date & time when the reading was continuously increasing for 30 minutes)

A PDF report of the analysis must be stored every week.
Notification must be sent when a new report is available.

## Tasks

### List Dependencies

List the dependencies of the Analysis-functionality.

1. Access to the Server containing the telemetrics in a csv file
2. Import libraries to perform read and write(if required) operation on CSV file
3. Import System Date and Time library
4. Import library for Off-the-shelf PDF converter to export analysis report as PDF file
5. Access to the particular API to create notifications
6. Access to cloud server to store PDF report of the analysis continuously during operation

### Mark the System Boundary

What is included in the software unit-test? What is not? Fill this table.

| Item                      | Included?     | Reasoning / Assumption
|---------------------------|---------------|---
Battery Data-accuracy       | No            | We do not test the accuracy of data
Computation of maximum      | Yes           | This is part of the software being developed
Off-the-shelf PDF converter | Yes           | We can use PDF converter API for testing
Counting the breaches       | Yes           | This is part of the software being developed
Detecting trends            | Yes           | This is part of the software being developed
Notification utility        | Yes           | This is part of the software being developed

### List the Test Cases

Write tests in the form of `<expected output or action>` from `<input>` / when `<event>`

Add to these tests:

1. Write minimum and maximum to the PDF from a csv containing positive and negative readings
2. Write "Invalid input" to the PDF when the csv doesn't contain expected data
3. Write the calculated result after Counting breaches to PDF file.
4. Write the calculated result after detecting trends to PDF file.
5. Write "Not Enough Data" if recording is less than 30 minutes.
6. Write "Hi, Battery Telemetrics new report is available" to notification API.

### Recognize Fakes and Reality

Consider the tests for each functionality below.
In those tests, identify inputs and outputs.
Enter one part that's real and another part that's faked/mocked.

| Functionality            | Input        | Output                      | Faked/mocked part
|--------------------------|--------------|-----------------------------|---
Read input from server     | csv file     | internal data-structure     | Fake the server store
Validate input             | csv data     | valid / invalid             | None - it's a pure function
Notify report availability | pdf file     | notification                | Fake the notification API call
Report inaccessible server | csv file     | notify server problem       | Fake the server store
Find minimum and maximum   | csv data     | minimum/maximum             | None - it's a pure function
Detect trend               | csv data     | date and time               | None - it's a pure function
Write to PDF               | csv data     | Analysis                    | Fake the PDF file
