---
layout: post
title:  "Blog-13-Jira-Bulk Create"
date:   2022-02-17 11:58:57 -0700
categories: Munki MDM Tool
---

This week I will be explianing how to use some features in Jira software.

<h1>JIRA</h1>
      Jira Software is part of a suite of solutions meant to assist teams of all sizes in managing their workloads. Jira was originally intended to be a bug and problem tracker. Jira, on the other hand, has matured into a strong task management application for various types of use cases, ranging from requirements and test case management to agile software development.

<h1>How to create a Jira Issue</h1>
      Jira can be used as a ticketing system to help companies keep track of issues, projects, and documentation.

      Keeping track of projects is one uneasy function you can use Jira for.

Buttt.

If we have multiple tickets  that we want to create there is a feature that helps create multiples tickets we use the Jira buclk create tool 
This a tool that grabs a .csv file and uses the data from the sheet to create muiltles fields for the ticket issue and others. Example − Summary, Assignee, Reporter, Priority, Description, Epic, “Windows”, or more.

<h1>Step 0:</h1>
When prparing your CSV you should have a heading row with a summary column. The first row is the heading row and represents the fields of the create issue page. 

<h1>Step 1:</h1>
When using the interface to use the bulk create tool, YOU will want to navigate to the TAB "Issue" --> Import Issues From CVA

<img src="https://www.tutorialspoint.com/jira/images/csv_functionality.jpg" alt="Jira" width="460" height="345">

<h1> Step 2:</h1>
Now that we are in create setup page you will select "CSV Sourse File" . YOu dont need to worry about “Use an existing configuration file" this will be introduced later but not needed to import thes issues.

Click "Next" once you have selected CVS:
<img src="https://www.tutorialspoint.com/jira/images/csv_source_file.jpg" alt="Jira" width="460" height="345">

<h1>Step 3:</h1>
If the user checks the checkbox of “Use an existing configuration file”, JIRA will ask to specify an Existing Configuration File.
IN step 6 it will ask you if you want download the confifuration file so you dont have to select the feild again.

<img src="https://www.tutorialspoint.com/jira/images/bulk_create_setup.jpg" alt="Jira" width="460" height="345">

<h1>Step 4:</h1>
When you click the Next button, the CSV file import wizard's Settings stage will appear. Fill in all of the mandatory fields.
If the CSV file contains a character other than a comma as a separator, type that character in the CSV Delimiter field. 
If the separator is a 'Tab,' use the format '/t' to enter it.

<img src="https://www.tutorialspoint.com/jira/images/settings_of_csv_file.jpg" alt="Jira" width="460" height="345">

<h1>Step 5 :</h1>
The Next button will take you to the CSV file import wizard's Map field phase.
The JIRA summary field should be mapped to a CSV field. This guarantees that the issues are summarized.
<img src="https://www.tutorialspoint.com/jira/images/map_field_value.jpg" alt="Jira" width="460" height="345">

<h1>Step 6 :</h1>
The CSV file import wizard's Map values step will appear. The user can choose which specific CSV field values to match to which specific JIRA field value on this phase of the import procedure.
This page will display fields whose Map Field Value check boxes were selected in the previous stage.

The importer will map imported usernames from the CSV file to (lowercase) JIRA usernames if the CSV field has a username (e.g. Reporter or Assignee) 
and the Map Column Value check box for this field is not selected in the previous phase of the CSV file import wizard.
<img src="https://www.tutorialspoint.com/jira/images/how_to_map_values.jpg" alt="Jira" width="460" height="345">

<h1>Step 7 :</h1>
Jira provides a one-of-a-kind feature that allows you to validate your problem before you create it.
Green denotes that you have the ability to create all of your problems.
Red indicates that you have a problem with your CVS or field mapping.
If you have the improper issue field, Yellow will warn you.

<img src="https://www.tutorialspoint.com/jira/images/validation.jpg" alt="Jira" width="460" height="345">

<h1>Step 8 :</h1>
Now! We are ready to Import when validate has been a success, once created it was give you link to your created issues.

<img src="https://www.tutorialspoint.com/jira/images/issues_created_using_csv_file.jpg" alt="Jira" width="460" height="345">

<h1>Step 9 :</h1>
Click Created Issues and Spot check the information
<img src="https://www.tutorialspoint.com/jira/images/how_to_map_values.jpg" alt="Jira" width="460" height="345">


